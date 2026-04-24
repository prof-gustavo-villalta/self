---
layout: material
title: "Material 11 - Sensores do Dispositivo"
---

# 📱 Sensores do Dispositivo: Acelerômetro, Giroscópio e Mais

Guia completo para acessar e utilizar os sensores do smartphone em Flutter,
incluindo acelerômetro, giroscópio, magnetômetro e sensor de proximidade.

---

## Sensores Disponíveis

| Sensor           | Função                               | Uso Comum                     |
| ---------------- | ------------------------------------ | ----------------------------- |
| **Acelerômetro** | Detecta aceleração nos eixos X, Y, Z | Shake, passos, inclinação     |
| **Giroscópio**   | Detecta rotação angular              | Jogos, realidade virtual      |
| **Magnetômetro** | Detecta campos magnéticos            | Bússola, orientação           |
| **Barômetro**    | Mede pressão atmosférica             | Altitude, previsão do tempo   |
| **Proximidade**  | Detecta objetos próximos             | Desligar tela durante ligação |
| **Luminosidade** | Mede luz ambiente                    | Ajuste automático de brilho   |

---

## Configuração

### Dependências

```yaml
dependencies:
  flutter:
    sdk: flutter
  sensors_plus: ^4.0.2
```

Execute:

```bash
flutter pub get
```

### Permissões

Geralmente **não são necessárias permissões especiais** para acessar sensores,
mas adicione no `AndroidManifest.xml`:

```xml
<!-- Opcional - para alta frequência de amostragem -->
<uses-permission android:name="android.permission.HIGH_SAMPLING_RATE_SENSORS" />
```

---

## Implementação

### 1. Acelerômetro

Detecta movimento e inclinação do dispositivo.

```dart
import 'package:flutter/material.dart';
import 'dart:async';
import 'dart:math' as math;
import 'package:sensors_plus/sensors_plus.dart';

class AcelerometroScreen extends StatefulWidget {
  const AcelerometroScreen({super.key});

  @override
  State<AcelerometroScreen> createState() => _AcelerometroScreenState();
}

class _AcelerometroScreenState extends State<AcelerometroScreen> {
  AccelerometerEvent? _accelerometerValues;
  StreamSubscription<AccelerometerEvent>? _accelerometerSubscription;

  // Para detectar shake
  DateTime? _lastShake;
  int _shakeCount = 0;

  @override
  void initState() {
    super.initState();
    _initAccelerometer();
  }

  void _initAccelerometer() {
    _accelerometerSubscription = accelerometerEvents.listen((event) {
      setState(() {
        _accelerometerValues = event;
      });
      _detectShake(event);
    });
  }

  // Algoritmo para detectar shake
  void _detectShake(AccelerometerEvent event) {
    final double gX = event.x / 9.80665;
    final double gY = event.y / 9.80665;
    final double gZ = event.z / 9.80665;

    // Força G (gravidade)
    double gForce = math.sqrt(gX * gX + gY * gY + gZ * gZ);

    if (gForce > 2.7) { // Threshold para shake
      final now = DateTime.now();
      if (_lastShake == null || now.difference(_lastShake!) > const Duration(milliseconds: 800)) {
        setState(() {
          _shakeCount++;
          _lastShake = now;
        });

        // Feedback visual
        ScaffoldMessenger.of(context).showSnackBar(
          const SnackBar(
            content: Text('🎉 Shake detectado!'),
            duration: Duration(milliseconds: 500),
          ),
        );
      }
    }
  }

  @override
  void dispose() {
    _accelerometerSubscription?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Acelerômetro'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          // Visualização dos valores
          Card(
            margin: const EdgeInsets.all(16),
            child: Padding(
              padding: const EdgeInsets.all(20),
              child: Column(
                children: [
                  const Text(
                    'Valores do Acelerômetro',
                    style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                  ),
                  const SizedBox(height: 16),
                  _buildAxisRow('X', _accelerometerValues?.x ?? 0, Colors.red),
                  const SizedBox(height: 8),
                  _buildAxisRow('Y', _accelerometerValues?.y ?? 0, Colors.green),
                  const SizedBox(height: 8),
                  _buildAxisRow('Z', _accelerometerValues?.z ?? 0, Colors.blue),
                ],
              ),
            ),
          ),

          // Visualização gráfica
          Container(
            margin: const EdgeInsets.all(16),
            height: 200,
            decoration: BoxDecoration(
              border: Border.all(color: Colors.grey),
              borderRadius: BorderRadius.circular(8),
            ),
            child: CustomPaint(
              size: const Size(double.infinity, 200),
              painter: AccelerometerPainter(
                x: _accelerometerValues?.x ?? 0,
                y: _accelerometerValues?.y ?? 0,
              ),
            ),
          ),

          // Contador de shakes
          Card(
            color: Colors.orange[100],
            child: Padding(
              padding: const EdgeInsets.all(16),
              child: Column(
                children: [
                  const Icon(Icons.vibration, size: 40),
                  const SizedBox(height: 8),
                  Text(
                    'Shakes detectados:',
                    style: TextStyle(color: Colors.orange[800]),
                  ),
                  Text(
                    '$_shakeCount',
                    style: TextStyle(
                      fontSize: 36,
                      fontWeight: FontWeight.bold,
                      color: Colors.orange[800],
                    ),
                  ),
                  const Text('Agite o celular!'),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildAxisRow(String label, double value, Color color) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Container(
          width: 30,
          height: 30,
          decoration: BoxDecoration(
            color: color,
            borderRadius: BorderRadius.circular(4),
          ),
          child: Center(
            child: Text(
              label,
              style: const TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),
        ),
        const SizedBox(width: 16),
        SizedBox(
          width: 100,
          child: Text(
            value.toStringAsFixed(2),
            style: const TextStyle(fontSize: 20, fontFamily: 'monospace'),
          ),
        ),
        const Text('m/s²'),
      ],
    );
  }
}

// Custom Painter para visualização
class AccelerometerPainter extends CustomPainter {
  final double x;
  final double y;

  AccelerometerPainter({required this.x, required this.y});

  @override
  void paint(Canvas canvas, Size size) {
    final centerX = size.width / 2;
    final centerY = size.height / 2;

    // Desenhar círculo central
    final paint = Paint()
      ..color = Colors.grey[300]!
      ..style = PaintingStyle.fill;
    canvas.drawCircle(Offset(centerX, centerY), 50, paint);

    // Desenhar borda
    final borderPaint = Paint()
      ..color = Colors.grey
      ..style = PaintingStyle.stroke
      ..strokeWidth = 2;
    canvas.drawCircle(Offset(centerX, centerY), 50, borderPaint);

    // Desenhar posição do acelerômetro
    final positionPaint = Paint()
      ..color = Colors.blue
      ..style = PaintingStyle.fill;

    // Mapear valores (-10 a 10) para o canvas
    final posX = centerX + (x * 5).clamp(-40, 40);
    final posY = centerY + (y * 5).clamp(-40, 40);

    canvas.drawCircle(Offset(posX, posY), 10, positionPaint);

    // Desenhar linhas de referência
    final linePaint = Paint()
      ..color = Colors.grey[400]!
      ..strokeWidth = 1;

    canvas.drawLine(
      Offset(centerX, 0),
      Offset(centerX, size.height),
      linePaint,
    );
    canvas.drawLine(
      Offset(0, centerY),
      Offset(size.width, centerY),
      linePaint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => true;
}
```

### 2. Giroscópio

Detecta rotação do dispositivo.

```dart
class GiroscopioScreen extends StatefulWidget {
  const GiroscopioScreen({super.key});

  @override
  State<GiroscopioScreen> createState() => _GiroscopioScreenState();
}

class _GiroscopioScreenState extends State<GiroscopioScreen> {
  GyroscopeEvent? _gyroscopeValues;
  StreamSubscription<GyroscopeEvent>? _gyroscopeSubscription;

  @override
  void initState() {
    super.initState();
    _gyroscopeSubscription = gyroscopeEvents.listen((event) {
      setState(() {
        _gyroscopeValues = event;
      });
    });
  }

  @override
  void dispose() {
    _gyroscopeSubscription?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Giroscópio')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Text(
              'Rotação Angular',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 20),
            _buildRotationRow('X (Roll)', _gyroscopeValues?.x ?? 0, Icons.rotate_left),
            const SizedBox(height: 12),
            _buildRotationRow('Y (Pitch)', _gyroscopeValues?.y ?? 0, Icons.rotate_right),
            const SizedBox(height: 12),
            _buildRotationRow('Z (Yaw)', _gyroscopeValues?.z ?? 0, Icons.rotate_90_degrees_ccw),
            const SizedBox(height: 40),
            const Icon(Icons.phone_android, size: 100, color: Colors.blue),
            const Text('Gire o dispositivo'),
          ],
        ),
      ),
    );
  }

  Widget _buildRotationRow(String label, double value, IconData icon) {
    return Card(
      margin: const EdgeInsets.symmetric(horizontal: 32),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Row(
          children: [
            Icon(icon, size: 32, color: Colors.blue),
            const SizedBox(width: 16),
            Expanded(
              child: Text(label, style: const TextStyle(fontSize: 16)),
            ),
            Text(
              '${value.toStringAsFixed(3)} rad/s',
              style: const TextStyle(fontSize: 16, fontFamily: 'monospace'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### 3. Tela Completa com Todos os Sensores

```dart
class SensoresScreen extends StatefulWidget {
  const SensoresScreen({super.key});

  @override
  State<SensoresScreen> createState() => _SensoresScreenState();
}

class _SensoresScreenState extends State<SensoresScreen> {
  AccelerometerEvent? _accelerometer;
  GyroscopeEvent? _gyroscope;
  MagnetometerEvent? _magnetometer;

  StreamSubscription<AccelerometerEvent>? _accelSubscription;
  StreamSubscription<GyroscopeEvent>? _gyroSubscription;
  StreamSubscription<MagnetometerEvent>? _magnetSubscription;

  @override
  void initState() {
    super.initState();
    _initSensors();
  }

  void _initSensors() {
    _accelSubscription = accelerometerEvents.listen((event) {
      setState(() => _accelerometer = event);
    });

    _gyroSubscription = gyroscopeEvents.listen((event) {
      setState(() => _gyroscope = event);
    });

    _magnetSubscription = magnetometerEvents.listen((event) {
      setState(() => _magnetometer = event);
    });
  }

  // Calcular direção da bússola
  double _calculateHeading() {
    if (_accelerometer == null || _magnetometer == null) return 0;

    double ax = _accelerometer!.x;
    double ay = _accelerometer!.y;
    double az = _accelerometer!.z;

    double mx = _magnetometer!.x;
    double my = _magnetometer!.y;
    double mz = _magnetometer!.z;

    // Calcular heading (simplificado)
    double heading = math.atan2(my, mx) * (180 / math.pi);
    return heading < 0 ? heading + 360 : heading;
  }

  @override
  void dispose() {
    _accelSubscription?.cancel();
    _gyroSubscription?.cancel();
    _magnetSubscription?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Todos os Sensores'),
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            // Acelerômetro
            _buildSensorCard(
              'Acelerômetro',
              Icons.speed,
              Colors.red,
              'X: ${_accelerometer?.x.toStringAsFixed(2) ?? 0}\n'
              'Y: ${_accelerometer?.y.toStringAsFixed(2) ?? 0}\n'
              'Z: ${_accelerometer?.z.toStringAsFixed(2) ?? 0}',
            ),

            const SizedBox(height: 12),

            // Giroscópio
            _buildSensorCard(
              'Giroscópio',
              Icons.rotate_right,
              Colors.green,
              'X: ${_gyroscope?.x.toStringAsFixed(3) ?? 0}\n'
              'Y: ${_gyroscope?.y.toStringAsFixed(3) ?? 0}\n'
              'Z: ${_gyroscope?.z.toStringAsFixed(3) ?? 0}',
            ),

            const SizedBox(height: 12),

            // Magnetômetro
            _buildSensorCard(
              'Magnetômetro (Bússola)',
              Icons.explore,
              Colors.blue,
              'X: ${_magnetometer?.x.toStringAsFixed(2) ?? 0}\n'
              'Y: ${_magnetometer?.y.toStringAsFixed(2) ?? 0}\n'
              'Z: ${_magnetometer?.z.toStringAsFixed(2) ?? 0}\n\n'
              'Direção: ${_calculateHeading().toStringAsFixed(1)}°',
            ),

            const SizedBox(height: 24),

            // Aplicações
            const Card(
              child: Padding(
                padding: EdgeInsets.all(16),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      'Aplicações Práticas',
                      style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                    ),
                    SizedBox(height: 12),
                    ListTile(
                      leading: Icon(Icons.gamepad),
                      title: Text('Jogos'),
                      subtitle: Text('Controle por movimento'),
                    ),
                    ListTile(
                      leading: Icon(Icons.directions_walk),
                      title: Text('Contador de Passos'),
                      subtitle: Text('Fitness e saúde'),
                    ),
                    ListTile(
                      leading: Icon(Icons.screen_rotation),
                      title: Text('Rotação de Tela'),
                      subtitle: Text('Portrait/Landscape automático'),
                    ),
                    ListTile(
                      leading: Icon(Icons.map),
                      title: Text('Realidade Aumentada'),
                      subtitle: Text('Posicionamento de objetos'),
                    ),
                  ],
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildSensorCard(String title, IconData icon, Color color, String values) {
    return Card(
      elevation: 4,
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Row(
          children: [
            Container(
              padding: const EdgeInsets.all(12),
              decoration: BoxDecoration(
                color: color.withOpacity(0.2),
                borderRadius: BorderRadius.circular(12),
              ),
              child: Icon(icon, color: color, size: 32),
            ),
            const SizedBox(width: 16),
            Expanded(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    title,
                    style: const TextStyle(
                      fontSize: 16,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 4),
                  Text(
                    values,
                    style: const TextStyle(
                      fontSize: 14,
                      fontFamily: 'monospace',
                    ),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Aplicações Práticas

### 1. Contador de Passos

```dart
class StepCounter {
  int stepCount = 0;
  DateTime? _lastStep;
  double _previousMagnitude = 0;

  void processAccelerometer(AccelerometerEvent event) {
    // Calcular magnitude vetorial
    double magnitude = math.sqrt(
      event.x * event.x + event.y * event.y + event.z * event.z,
    );

    // Detectar pico (passo)
    double delta = magnitude - _previousMagnitude;
    _previousMagnitude = magnitude;

    if (delta > 12) { // Threshold para passo
      final now = DateTime.now();
      if (_lastStep == null || now.difference(_lastStep!) > const Duration(milliseconds: 300)) {
        stepCount++;
        _lastStep = now;
      }
    }
  }
}
```

### 2. Nível de Bolha (Bubble Level)

```dart
class BubbleLevelPainter extends CustomPainter {
  final double x;
  final double y;

  BubbleLevelPainter({required this.x, required this.y});

  @override
  void paint(Canvas canvas, Size size) {
    final center = Offset(size.width / 2, size.height / 2);

    // Círculo externo
    canvas.drawCircle(
      center,
      size.width / 2 - 20,
      Paint()
        ..color = Colors.grey[300]!
        ..style = PaintingStyle.fill,
    );

    // Marcas de nível
    final markPaint = Paint()
      ..color = Colors.grey
      ..strokeWidth = 2;

    canvas.drawLine(
      Offset(center.dx - 10, center.dy),
      Offset(center.dx + 10, center.dy),
      markPaint,
    );
    canvas.drawLine(
      Offset(center.dx, center.dy - 10),
      Offset(center.dx, center.dy + 10),
      markPaint,
    );

    // Bolha
    final bubbleX = center.dx + (x * 10).clamp(-100, 100);
    final bubbleY = center.dy + (y * 10).clamp(-100, 100);

    final isLevel = x.abs() < 0.5 && y.abs() < 0.5;

    canvas.drawCircle(
      Offset(bubbleX, bubbleY),
      20,
      Paint()
        ..color = isLevel ? Colors.green : Colors.red
        ..style = PaintingStyle.fill,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => true;
}
```

---

## Boas Práticas

1. **Sempre cancele as subscriptions** no dispose()
2. **Use filtros** para evitar processamento excessivo
3. **Considere a bateria** - sensores consomem energia
4. **Trate valores nulos** - sensores podem não estar disponíveis
5. **Teste em dispositivos reais** - emuladores têm simulação limitada

---

## Troubleshooting

| Problema            | Solução                                           |
| ------------------- | ------------------------------------------------- |
| Valores sempre zero | Teste em dispositivo físico                       |
| Valores instáveis   | Implemente filtro de média móvel                  |
| Alta latência       | Use `UserAccelerometerEvent` para dados filtrados |
| Consumo de bateria  | Pause subscriptions quando app em background      |

---

## Referências

- **sensors_plus:**
  [pub.dev/packages/sensors_plus](https://pub.dev/packages/sensors_plus)
- **Android Sensors:**
  [developer.android.com/guide/topics/sensors](https://developer.android.com/guide/topics/sensors/sensors_overview)
- **Sensor Coordinate System:**
  [developer.android.com/guide/topics/sensors/sensors_overview#sensors-coords](https://developer.android.com/guide/topics/sensors/sensors_overview#sensors-coords)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
