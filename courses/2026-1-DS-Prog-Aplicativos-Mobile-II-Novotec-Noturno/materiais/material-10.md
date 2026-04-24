---
layout: material
title: "Material 10 - Bluetooth e Comunicação com Dispositivos"
---

# 🔵 Bluetooth: Comunicação com Dispositivos Embarcados

Guia completo para integração Bluetooth em Flutter, permitindo comunicação com
Arduino, sensores e outros dispositivos embarcados.

---

## Tipos de Bluetooth

| Tipo                  | Alcance | Velocidade        | Uso                           |
| --------------------- | ------- | ----------------- | ----------------------------- |
| **Bluetooth Classic** | ~100m   | 1-3 Mbps          | Transmissão contínua de dados |
| **BLE (Low Energy)**  | ~100m   | 125 Kbps - 2 Mbps | Baixo consumo, sensores IoT   |

### Quando usar cada um?

- **Classic:** Arquivos grandes, áudio, streaming
- **BLE:** Sensores, wearables, beacons, IoT

---

## Configuração

### Dependências

Para Bluetooth Classic:

```yaml
dependencies:
  flutter_bluetooth_serial: ^0.4.0
  permission_handler: ^11.3.0
```

Para BLE (alternativa):

```yaml
dependencies:
  flutter_blue_plus: ^1.31.0
  permission_handler: ^11.3.0
```

Execute:

```bash
flutter pub get
```

### Permissões Android

No `AndroidManifest.xml`:

```xml
<!-- Para Android 11 e inferior -->
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

<!-- Para Android 12+ (API 31+) -->
<uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
<uses-permission android:name="android.permission.BLUETOOTH_ADVERTISE" />

<!-- Feature declaration -->
<uses-feature android:name="android.hardware.bluetooth" android:required="true" />
```

---

## Implementação Bluetooth Classic

### 1. Service de Bluetooth

```dart
import 'dart:async';
import 'dart:convert';
import 'dart:typed_data';
import 'package:flutter_bluetooth_serial/flutter_bluetooth_serial.dart';
import 'package:permission_handler/permission_handler.dart';

class BluetoothService {
  final FlutterBluetoothSerial _bluetooth = FlutterBluetoothSerial.instance;
  BluetoothConnection? _connection;

  final _dataController = StreamController<String>.broadcast();
  final _connectionController = StreamController<bool>.broadcast();

  bool _isConnected = false;
  List<BluetoothDevice> _pairedDevices = [];

  // Streams
  Stream<String> get dataStream => _dataController.stream;
  Stream<bool> get connectionStream => _connectionController.stream;
  bool get isConnected => _isConnected;
  List<BluetoothDevice> get pairedDevices => _pairedDevices;

  // Solicitar permissões
  Future<bool> requestPermissions() async {
    Map<Permission, PermissionStatus> statuses = await [
      Permission.bluetooth,
      Permission.bluetoothScan,
      Permission.bluetoothConnect,
      Permission.location,
    ].request();

    return statuses.values.every((status) => status.isGranted);
  }

  // Verificar se Bluetooth está ativado
  Future<bool> isEnabled() async {
    return await _bluetooth.isEnabled ?? false;
  }

  // Pedir para ativar Bluetooth
  Future<void> enable() async {
    await _bluetooth.requestEnable();
  }

  // Listar dispositivos pareados
  Future<List<BluetoothDevice>> getPairedDevices() async {
    _pairedDevices = await _bluetooth.getBondedDevices();
    return _pairedDevices;
  }

  // Conectar a um dispositivo
  Future<bool> connect(BluetoothDevice device) async {
    try {
      _connection = await BluetoothConnection.toAddress(device.address);

      if (_connection!.isConnected) {
        _isConnected = true;
        _connectionController.add(true);

        // Ouvir dados recebidos
        _connection!.input!.listen(
          (Uint8List data) {
            String message = utf8.decode(data);
            _dataController.add(message);
          },
          onDone: () {
            disconnect();
          },
          onError: (error) {
            print('Erro na comunicação: $error');
            disconnect();
          },
        );

        return true;
      }
    } catch (e) {
      print('Erro ao conectar: $e');
    }
    return false;
  }

  // Enviar dados
  Future<void> sendData(String data) async {
    if (_isConnected && _connection != null) {
      Uint8List bytes = Uint8List.fromList(utf8.encode(data + '\n'));
      _connection!.output.add(bytes);
      await _connection!.output.allSent;
    }
  }

  // Enviar comando simples
  Future<void> sendCommand(String command) async {
    await sendData(command);
  }

  // Desconectar
  Future<void> disconnect() async {
    if (_connection != null) {
      await _connection!.close();
      _connection = null;
    }
    _isConnected = false;
    _connectionController.add(false);
  }

  void dispose() {
    disconnect();
    _dataController.close();
    _connectionController.close();
  }
}
```

### 2. Tela de Controle Bluetooth

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bluetooth_serial/flutter_bluetooth_serial.dart';
import '../services/bluetooth_service.dart';

class BluetoothScreen extends StatefulWidget {
  const BluetoothScreen({super.key});

  @override
  State<BluetoothScreen> createState() => _BluetoothScreenState();
}

class _BluetoothScreenState extends State<BluetoothScreen> {
  final BluetoothService _bluetoothService = BluetoothService();
  List<BluetoothDevice> _devices = [];
  bool _isScanning = false;
  bool _isConnected = false;
  BluetoothDevice? _connectedDevice;

  String _receivedData = '';
  final TextEditingController _commandController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _initBluetooth();
  }

  Future<void> _initBluetooth() async {
    // Solicitar permissões
    bool hasPermission = await _bluetoothService.requestPermissions();
    if (!hasPermission) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Permissões necessárias')),
      );
      return;
    }

    // Verificar se Bluetooth está ativo
    bool isEnabled = await _bluetoothService.isEnabled();
    if (!isEnabled) {
      await _bluetoothService.enable();
    }

    // Ouvir mudanças de conexão
    _bluetoothService.connectionStream.listen((connected) {
      setState(() => _isConnected = connected);
    });

    // Ouvir dados recebidos
    _bluetoothService.dataStream.listen((data) {
      setState(() {
        _receivedData += '$data\n';
      });
    });

    _loadPairedDevices();
  }

  Future<void> _loadPairedDevices() async {
    setState(() => _isScanning = true);
    _devices = await _bluetoothService.getPairedDevices();
    setState(() => _isScanning = false);
  }

  Future<void> _connectToDevice(BluetoothDevice device) async {
    showDialog(
      context: context,
      barrierDismissible: false,
      builder: (_) => const Center(child: CircularProgressIndicator()),
    );

    bool success = await _bluetoothService.connect(device);

    Navigator.pop(context);

    if (success) {
      setState(() {
        _connectedDevice = device;
        _isConnected = true;
      });
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Conectado a ${device.name}')),
      );
    } else {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Falha na conexão')),
      );
    }
  }

  Future<void> _sendCommand() async {
    String command = _commandController.text.trim();
    if (command.isEmpty) return;

    await _bluetoothService.sendCommand(command);
    _commandController.clear();
  }

  @override
  void dispose() {
    _bluetoothService.dispose();
    _commandController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Controle Bluetooth'),
        actions: [
          IconButton(
            icon: const Icon(Icons.refresh),
            onPressed: _isScanning ? null : _loadPairedDevices,
          ),
          IconButton(
            icon: Icon(_isConnected ? Icons.bluetooth_connected : Icons.bluetooth),
            color: _isConnected ? Colors.blue : null,
            onPressed: () {
              if (_isConnected) {
                _bluetoothService.disconnect();
              }
            },
          ),
        ],
      ),
      body: Column(
        children: [
          // Status
          Container(
            padding: const EdgeInsets.all(16),
            color: _isConnected ? Colors.green[100] : Colors.grey[200],
            child: Row(
              children: [
                Icon(
                  _isConnected ? Icons.check_circle : Icons.bluetooth_searching,
                  color: _isConnected ? Colors.green : Colors.grey,
                ),
                const SizedBox(width: 8),
                Expanded(
                  child: Text(
                    _isConnected
                        ? 'Conectado: ${_connectedDevice?.name ?? "Desconhecido"}'
                        : 'Desconectado',
                    style: const TextStyle(fontWeight: FontWeight.bold),
                  ),
                ),
              ],
            ),
          ),

          // Lista de dispositivos ou Controles
          Expanded(
            child: _isConnected ? _buildControls() : _buildDeviceList(),
          ),
        ],
      ),
    );
  }

  Widget _buildDeviceList() {
    if (_isScanning) {
      return const Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            CircularProgressIndicator(),
            SizedBox(height: 16),
            Text('Buscando dispositivos...'),
          ],
        ),
      );
    }

    if (_devices.isEmpty) {
      return const Center(
        child: Text(
          'Nenhum dispositivo pareado encontrado\n'
          'Vá em Configurações > Bluetooth para parear',
          textAlign: TextAlign.center,
        ),
      );
    }

    return ListView.builder(
      itemCount: _devices.length,
      itemBuilder: (context, index) {
        BluetoothDevice device = _devices[index];
        return ListTile(
          leading: const Icon(Icons.devices),
          title: Text(device.name ?? 'Dispositivo desconhecido'),
          subtitle: Text(device.address),
          trailing: ElevatedButton(
            onPressed: () => _connectToDevice(device),
            child: const Text('Conectar'),
          ),
        );
      },
    );
  }

  Widget _buildControls() {
    return Column(
      children: [
        // Comandos rápidos
        Padding(
          padding: const EdgeInsets.all(16),
          child: Wrap(
            spacing: 8,
            runSpacing: 8,
            children: [
              ElevatedButton.icon(
                onPressed: () => _bluetoothService.sendCommand('LED_ON'),
                icon: const Icon(Icons.lightbulb),
                label: const Text('LED ON'),
              ),
              ElevatedButton.icon(
                onPressed: () => _bluetoothService.sendCommand('LED_OFF'),
                icon: const Icon(Icons.lightbulb_outline),
                label: const Text('LED OFF'),
              ),
              ElevatedButton.icon(
                onPressed: () => _bluetoothService.sendCommand('READ_TEMP'),
                icon: const Icon(Icons.thermostat),
                label: const Text('Temperatura'),
              ),
              ElevatedButton.icon(
                onPressed: () => _bluetoothService.sendCommand('STATUS'),
                icon: const Icon(Icons.info),
                label: const Text('Status'),
              ),
            ],
          ),
        ),

        // Comando personalizado
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 16),
          child: Row(
            children: [
              Expanded(
                child: TextField(
                  controller: _commandController,
                  decoration: const InputDecoration(
                    labelText: 'Comando personalizado',
                    hintText: 'Digite o comando...',
                    border: OutlineInputBorder(),
                  ),
                ),
              ),
              const SizedBox(width: 8),
              ElevatedButton(
                onPressed: _sendCommand,
                child: const Icon(Icons.send),
              ),
            ],
          ),
        ),

        // Dados recebidos
        Expanded(
          child: Container(
            margin: const EdgeInsets.all(16),
            padding: const EdgeInsets.all(12),
            decoration: BoxDecoration(
              color: Colors.black87,
              borderRadius: BorderRadius.circular(8),
            ),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                const Text(
                  'DADOS RECEBIDOS:',
                  style: TextStyle(
                    color: Colors.green,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                const Divider(color: Colors.green),
                Expanded(
                  child: SingleChildScrollView(
                    child: Text(
                      _receivedData.isEmpty ? 'Aguardando dados...' : _receivedData,
                      style: const TextStyle(
                        color: Colors.green,
                        fontFamily: 'monospace',
                      ),
                    ),
                  ),
                ),
              ],
            ),
          ),
        ),

        // Botão desconectar
        Padding(
          padding: const EdgeInsets.all(16),
          child: ElevatedButton.icon(
            onPressed: () => _bluetoothService.disconnect(),
            icon: const Icon(Icons.bluetooth_disabled),
            label: const Text('Desconectar'),
            style: ElevatedButton.styleFrom(
              backgroundColor: Colors.red,
              foregroundColor: Colors.white,
            ),
          ),
        ),
      ],
    );
  }
}
```

---

## Código Arduino (Para Testes)

```cpp
#include <SoftwareSerial.h>

// Configuração Bluetooth (módulo HC-05/HC-06)
SoftwareSerial bluetooth(10, 11); // RX, TX

const int LED_PIN = 13;
String command = "";

void setup() {
  Serial.begin(9600);
  bluetooth.begin(9600);

  pinMode(LED_PIN, OUTPUT);

  Serial.println("Arduino pronto!");
  bluetooth.println("Arduino conectado!");
}

void loop() {
  // Ler comandos do Bluetooth
  if (bluetooth.available()) {
    char c = bluetooth.read();

    if (c == '\n') {
      processCommand(command);
      command = "";
    } else {
      command += c;
    }
  }

  // Ler do Serial e enviar por Bluetooth
  if (Serial.available()) {
    bluetooth.write(Serial.read());
  }
}

void processCommand(String cmd) {
  cmd.trim();
  cmd.toUpperCase();

  Serial.println("Comando recebido: " + cmd);

  if (cmd == "LED_ON") {
    digitalWrite(LED_PIN, HIGH);
    bluetooth.println("LED ligado!");
  }
  else if (cmd == "LED_OFF") {
    digitalWrite(LED_PIN, LOW);
    bluetooth.println("LED desligado!");
  }
  else if (cmd == "READ_TEMP") {
    int temp = analogRead(A0);
    float voltage = temp * 5.0 / 1023.0;
    float temperature = (voltage - 0.5) * 100;
    bluetooth.println("Temperatura: " + String(temperature) + " C");
  }
  else if (cmd == "STATUS") {
    bluetooth.println("Sistema OK - LED: " + String(digitalRead(LED_PIN)));
  }
  else {
    bluetooth.println("Comando desconhecido: " + cmd);
  }
}
```

---

## Protocolo de Comunicação

### Formato JSON (Recomendado)

```dart
// Enviar
{
  "command": "SET_LED",
  "params": {
    "pin": 13,
    "state": "ON"
  },
  "timestamp": 1234567890
}

// Receber
{
  "status": "OK",
  "data": {
    "temperature": 25.5,
    "humidity": 60
  },
  "timestamp": 1234567890
}
```

### Código de Parsing

```dart
import 'dart:convert';

void handleReceivedData(String data) {
  try {
    Map<String, dynamic> json = jsonDecode(data);

    switch (json['command']) {
      case 'SENSOR_DATA':
        double temp = json['data']['temperature'];
        double humidity = json['data']['humidity'];
        updateSensors(temp, humidity);
        break;
      case 'STATUS':
        String status = json['status'];
        print('Status do dispositivo: $status');
        break;
    }
  } catch (e) {
    print('Erro ao parsear JSON: $e');
  }
}
```

---

## Casos de Uso

| Aplicação                 | Descrição                                  |
| ------------------------- | ------------------------------------------ |
| **Automação Residencial** | Controlar luzes, portas, sensores          |
| **Indústria 4.0**         | Monitorar máquinas e equipamentos          |
| **Saúde**                 | Conectar com medidores de glicose, pressão |
| **Veículos**              | Diagnosticar OBD2, telemetria              |
| **Agricultura**           | Sensores de umidade, irrigação             |

---

## Troubleshooting

| Problema                   | Solução                                             |
| -------------------------- | --------------------------------------------------- |
| "Bluetooth não disponível" | Verificar permissões no Android 12+                 |
| Não encontra dispositivos  | Parear primeiro nas configurações do Android        |
| Conexão cai                | Verificar alimentação do módulo Bluetooth           |
| Dados corrompidos          | Verificar baud rate (deve ser igual nos dois lados) |
| Lentidão                   | Usar baud rate maior (57600 ou 115200)              |

---

## Referências

- **flutter_bluetooth_serial:**
  [pub.dev/packages/flutter_bluetooth_serial](https://pub.dev/packages/flutter_bluetooth_serial)
- **flutter_blue_plus:**
  [pub.dev/packages/flutter_blue_plus](https://pub.dev/packages/flutter_blue_plus)
- **Bluetooth SPP:**
  [developer.android.com/guide/topics/connectivity/bluetooth](https://developer.android.com/guide/topics/connectivity/bluetooth)
- **Arduino Bluetooth:** [docs.arduino.cc](https://docs.arduino.cc/)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
