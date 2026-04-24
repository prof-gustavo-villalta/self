---
layout: material
title: "Material 12 - Telefonia e SMS"
---

# 📞 Telefonia e SMS

Guia completo para integrar recursos de telefonia e mensagens SMS em aplicativos
Flutter, incluindo discagem, envio de SMS e leitura de contatos.

---

## Funcionalidades Cobertas

| Funcionalidade     | Pacote             | Uso                |
| ------------------ | ------------------ | ------------------ |
| Fazer ligações     | `url_launcher`     | Discar números     |
| Enviar SMS         | `flutter_sms`      | Mensagens de texto |
| Ler contatos       | `contacts_service` | Agenda telefônica  |
| Informações do SIM | `mobile_number`    | Dados do chip      |

---

## Configuração

### Dependências

```yaml
dependencies:
  flutter:
    sdk: flutter
  url_launcher: ^6.2.5
  flutter_sms: ^2.3.3
  contacts_service: ^0.6.3
  permission_handler: ^11.3.0
```

Execute:

```bash
flutter pub get
```

### Permissões Android

No `AndroidManifest.xml`:

```xml
<!-- Para fazer ligações -->
<uses-permission android:name="android.permission.CALL_PHONE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />

<!-- Para enviar SMS -->
<uses-permission android:name="android.permission.SEND_SMS" />
<uses-permission android:name="android.permission.READ_SMS" />

<!-- Para ler contatos -->
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.WRITE_CONTACTS" />

<!-- Para verificar se pode fazer ligação -->
<uses-feature android:name="android.hardware.telephony" android:required="false" />
```

---

## 1. Fazer Ligações

### Implementação

```dart
import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

class TelefoneService {
  // Abrir discador com número
  static Future<void> discar(String numero) async {
    final Uri url = Uri(scheme: 'tel', path: numero);

    if (await canLaunchUrl(url)) {
      await launchUrl(url);
    } else {
      throw 'Não foi possível discar $numero';
    }
  }

  // Fazer ligação direta (requer permissão CALL_PHONE)
  static Future<void> ligarDireto(String numero) async {
    final Uri url = Uri(scheme: 'tel', path: numero);

    if (await canLaunchUrl(url)) {
      await launchUrl(
        url,
        mode: LaunchMode.externalApplication,
      );
    }
  }
}
```

### Tela de Discagem

```dart
class DiscadorScreen extends StatefulWidget {
  const DiscadorScreen({super.key});

  @override
  State<DiscadorScreen> createState() => _DiscadorScreenState();
}

class _DiscadorScreenState extends State<DiscadorScreen> {
  String _numero = '';

  void _adicionarDigito(String digito) {
    setState(() {
      _numero += digito;
    });
  }

  void _removerDigito() {
    if (_numero.isNotEmpty) {
      setState(() {
        _numero = _numero.substring(0, _numero.length - 1);
      });
    }
  }

  Future<void> _fazerLigacao() async {
    if (_numero.isEmpty) return;

    try {
      await TelefoneService.discar(_numero);
    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro: $e')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Discador')),
      body: Column(
        children: [
          // Display do número
          Container(
            padding: const EdgeInsets.all(32),
            alignment: Alignment.center,
            child: Text(
              _numero.isEmpty ? 'Digite o número' : _numero,
              style: TextStyle(
                fontSize: _numero.isEmpty ? 24 : 36,
                fontWeight: FontWeight.bold,
                color: _numero.isEmpty ? Colors.grey : Colors.black,
              ),
            ),
          ),

          // Teclado numérico
          Expanded(
            child: GridView.count(
              crossAxisCount: 3,
              childAspectRatio: 1.5,
              padding: const EdgeInsets.all(16),
              children: [
                ...['1', '2', '3', '4', '5', '6', '7', '8', '9', '*', '0', '#']
                    .map((digito) => _buildTecla(digito)),
              ],
            ),
          ),

          // Botões de ação
          Padding(
            padding: const EdgeInsets.all(16),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                IconButton(
                  icon: const Icon(Icons.backspace, size: 32),
                  onPressed: _removerDigito,
                ),
                FloatingActionButton(
                  onPressed: _fazerLigacao,
                  backgroundColor: Colors.green,
                  child: const Icon(Icons.phone, size: 32),
                ),
                const SizedBox(width: 48), // Espaçamento
              ],
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildTecla(String digito) {
    return InkWell(
      onTap: () => _adicionarDigito(digito),
      child: Container(
        margin: const EdgeInsets.all(8),
        decoration: BoxDecoration(
          color: Colors.grey[200],
          borderRadius: BorderRadius.circular(12),
        ),
        child: Center(
          child: Text(
            digito,
            style: const TextStyle(fontSize: 28, fontWeight: FontWeight.bold),
          ),
        ),
      ),
    );
  }
}
```

---

## 2. Enviar SMS

### Implementação

```dart
import 'package:flutter_sms/flutter_sms.dart';

class SmsService {
  // Enviar SMS usando app nativo
  static Future<void> enviarComApp(String mensagem, List<String> destinatarios) async {
    try {
      String result = await sendSMS(
        message: mensagem,
        recipients: destinatarios,
        sendDirect: false, // Abre o app de SMS nativo
      );
      print(result);
    } catch (e) {
      print('Erro ao enviar SMS: $e');
    }
  }

  // Enviar SMS diretamente (requer permissão SEND_SMS)
  static Future<void> enviarDireto(String mensagem, List<String> destinatarios) async {
    try {
      String result = await sendSMS(
        message: mensagem,
        recipients: destinatarios,
        sendDirect: true, // Envia sem abrir app
      );
      print(result);
    } catch (e) {
      print('Erro ao enviar SMS: $e');
    }
  }
}
```

### Tela de SMS

```dart
class EnviarSmsScreen extends StatefulWidget {
  const EnviarSmsScreen({super.key});

  @override
  State<EnviarSmsScreen> createState() => _EnviarSmsScreenState();
}

class _EnviarSmsScreenState extends State<EnviarSmsScreen> {
  final TextEditingController _numeroController = TextEditingController();
  final TextEditingController _mensagemController = TextEditingController();
  bool _enviando = false;
  int _caracteres = 0;
  int _smsCount = 1;

  @override
  void initState() {
    super.initState();
    _mensagemController.addListener(_atualizarContador);
  }

  void _atualizarContador() {
    setState(() {
      _caracteres = _mensagemController.text.length;
      // SMS padrão: 160 caracteres
      // SMS concatenado: 153 caracteres cada
      if (_caracteres <= 160) {
        _smsCount = 1;
      } else {
        _smsCount = (_caracteres / 153).ceil();
      }
    });
  }

  Future<void> _enviarSms() async {
    final numero = _numeroController.text.trim();
    final mensagem = _mensagemController.text.trim();

    if (numero.isEmpty || mensagem.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Preencha número e mensagem')),
      );
      return;
    }

    setState(() => _enviando = true);

    try {
      await SmsService.enviarComApp(mensagem, [numero]);

      if (mounted) {
        ScaffoldMessenger.of(context).showSnackBar(
          const SnackBar(content: Text('SMS enviado!')),
        );
        _mensagemController.clear();
      }
    } catch (e) {
      if (mounted) {
        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(content: Text('Erro: $e')),
        );
      }
    } finally {
      if (mounted) setState(() => _enviando = false);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Enviar SMS')),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            // Campo de número
            TextField(
              controller: _numeroController,
              keyboardType: TextInputType.phone,
              decoration: InputDecoration(
                labelText: 'Número do destinatário',
                hintText: '(11) 99999-9999',
                prefixIcon: const Icon(Icons.phone),
                border: const OutlineInputBorder(),
                suffixIcon: IconButton(
                  icon: const Icon(Icons.contacts),
                  onPressed: () {
                    // Abrir lista de contatos
                    _selecionarContato();
                  },
                ),
              ),
            ),

            const SizedBox(height: 16),

            // Campo de mensagem
            TextField(
              controller: _mensagemController,
              maxLines: 6,
              maxLength: 459, // 3 SMS
              decoration: const InputDecoration(
                labelText: 'Mensagem',
                hintText: 'Digite sua mensagem aqui...',
                border: OutlineInputBorder(),
                alignLabelWithHint: true,
              ),
            ),

            // Contador de caracteres
            Align(
              alignment: Alignment.centerRight,
              child: Text(
                '$_caracteres caracteres${_smsCount > 1 ? ' ($_smsCount SMS)' : ''}',
                style: TextStyle(
                  color: _smsCount > 1 ? Colors.orange : Colors.grey,
                ),
              ),
            ),

            const Spacer(),

            // Botão enviar
            SizedBox(
              width: double.infinity,
              height: 50,
              child: ElevatedButton.icon(
                onPressed: _enviando ? null : _enviarSms,
                icon: _enviando
                    ? const SizedBox(
                        width: 20,
                        height: 20,
                        child: CircularProgressIndicator(strokeWidth: 2, color: Colors.white),
                      )
                    : const Icon(Icons.send),
                label: Text(_enviando ? 'Enviando...' : 'Enviar SMS'),
              ),
            ),
          ],
        ),
      ),
    );
  }

  Future<void> _selecionarContato() async {
    // Implementação na próxima seção
  }

  @override
  void dispose() {
    _numeroController.dispose();
    _mensagemController.dispose();
    super.dispose();
  }
}
```

---

## 3. Ler Contatos

### Implementação

```dart
import 'package:contacts_service/contacts_service.dart';
import 'package:permission_handler/permission_handler.dart';

class ContatosService {
  // Solicitar permissão
  static Future<bool> solicitarPermissao() async {
    PermissionStatus status = await Permission.contacts.request();
    return status.isGranted;
  }

  // Buscar todos os contatos
  static Future<List<Contact>> buscarContatos() async {
    bool hasPermission = await solicitarPermissao();
    if (!hasPermission) {
      throw Exception('Permissão de contatos negada');
    }

    Iterable<Contact> contatos = await ContactsService.getContacts();
    return contatos.toList();
  }

  // Buscar contato por nome
  static Future<List<Contact>> buscarPorNome(String query) async {
    bool hasPermission = await solicitarPermissao();
    if (!hasPermission) return [];

    Iterable<Contact> contatos = await ContactsService.getContacts(query: query);
    return contatos.toList();
  }
}
```

### Tela de Seleção de Contatos

```dart
class SelecionarContatoScreen extends StatefulWidget {
  const SelecionarContatoScreen({super.key});

  @override
  State<SelecionarContatoScreen> createState() => _SelecionarContatoScreenState();
}

class _SelecionarContatoScreenState extends State<SelecionarContatoScreen> {
  List<Contact> _contatos = [];
  List<Contact> _contatosFiltrados = [];
  bool _carregando = true;
  final TextEditingController _buscaController = TextEditingController();

  @override
  void initState() {
    super.initState();
    _carregarContatos();
  }

  Future<void> _carregarContatos() async {
    try {
      List<Contact> contatos = await ContatosService.buscarContatos();
      setState(() {
        _contatos = contatos;
        _contatosFiltrados = contatos;
        _carregando = false;
      });
    } catch (e) {
      setState(() => _carregando = false);
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro: $e')),
      );
    }
  }

  void _filtrarContatos(String query) {
    setState(() {
      _contatosFiltrados = _contatos.where((contato) {
        String nome = contato.displayName ?? '';
        return nome.toLowerCase().contains(query.toLowerCase());
      }).toList();
    });
  }

  String _getNumeroPrincipal(Contact contato) {
    if (contato.phones != null && contato.phones!.isNotEmpty) {
      return contato.phones!.first.value ?? '';
    }
    return '';
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Selecionar Contato'),
      ),
      body: Column(
        children: [
          // Campo de busca
          Padding(
            padding: const EdgeInsets.all(8),
            child: TextField(
              controller: _buscaController,
              decoration: InputDecoration(
                hintText: 'Buscar contato...',
                prefixIcon: const Icon(Icons.search),
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(8),
                ),
              ),
              onChanged: _filtrarContatos,
            ),
          ),

          // Lista de contatos
          Expanded(
            child: _carregando
                ? const Center(child: CircularProgressIndicator())
                : _contatosFiltrados.isEmpty
                    ? const Center(child: Text('Nenhum contato encontrado'))
                    : ListView.builder(
                        itemCount: _contatosFiltrados.length,
                        itemBuilder: (context, index) {
                          Contact contato = _contatosFiltrados[index];
                          String numero = _getNumeroPrincipal(contato);

                          return ListTile(
                            leading: CircleAvatar(
                              backgroundColor: Colors.blue,
                              child: Text(
                                contato.initials,
                                style: const TextStyle(color: Colors.white),
                              ),
                            ),
                            title: Text(contato.displayName ?? 'Sem nome'),
                            subtitle: numero.isNotEmpty ? Text(numero) : null,
                            onTap: numero.isNotEmpty
                                ? () => Navigator.pop(context, numero)
                                : null,
                            trailing: numero.isNotEmpty
                                ? Row(
                                    mainAxisSize: MainAxisSize.min,
                                    children: [
                                      IconButton(
                                        icon: const Icon(Icons.message, color: Colors.blue),
                                        onPressed: () {
                                          Navigator.pop(context, {
                                            'numero': numero,
                                            'acao': 'sms',
                                          });
                                        },
                                      ),
                                      IconButton(
                                        icon: const Icon(Icons.phone, color: Colors.green),
                                        onPressed: () {
                                          Navigator.pop(context, {
                                            'numero': numero,
                                            'acao': 'ligar',
                                          });
                                        },
                                      ),
                                    ],
                                  )
                                : null,
                          );
                        },
                      ),
          ),
        ],
      ),
    );
  }
}
```

---

## Tela Integrada: Central de Comunicação

```dart
class CentralComunicacaoScreen extends StatelessWidget {
  const CentralComunicacaoScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Central de Comunicação'),
      ),
      body: GridView.count(
        crossAxisCount: 2,
        padding: const EdgeInsets.all(16),
        children: [
          _buildOpcao(
            context,
            'Discador',
            Icons.dialpad,
            Colors.blue,
            () => Navigator.push(
              context,
              MaterialPageRoute(builder: (_) => const DiscadorScreen()),
            ),
          ),
          _buildOpcao(
            context,
            'Enviar SMS',
            Icons.message,
            Colors.green,
            () => Navigator.push(
              context,
              MaterialPageRoute(builder: (_) => const EnviarSmsScreen()),
            ),
          ),
          _buildOpcao(
            context,
            'Contatos',
            Icons.contacts,
            Colors.orange,
            () => Navigator.push(
              context,
              MaterialPageRoute(builder: (_) => const SelecionarContatoScreen()),
            ),
          ),
          _buildOpcao(
            context,
            'Emergência',
            Icons.emergency,
            Colors.red,
            () => _mostrarEmergencia(context),
          ),
        ],
      ),
    );
  }

  Widget _buildOpcao(
    BuildContext context,
    String titulo,
    IconData icone,
    Color cor,
    VoidCallback onTap,
  ) {
    return Card(
      elevation: 4,
      child: InkWell(
        onTap: onTap,
        borderRadius: BorderRadius.circular(12),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(icone, size: 48, color: cor),
            const SizedBox(height: 12),
            Text(
              titulo,
              style: const TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
            ),
          ],
        ),
      ),
    );
  }

  void _mostrarEmergencia(BuildContext context) {
    showModalBottomSheet(
      context: context,
      builder: (context) => Container(
        padding: const EdgeInsets.all(16),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            const Text(
              'Números de Emergência',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 16),
            ListTile(
              leading: const Icon(Icons.local_police, color: Colors.red),
              title: const Text('Polícia Militar'),
              subtitle: const Text('190'),
              trailing: const Icon(Icons.phone),
              onTap: () => TelefoneService.discar('190'),
            ),
            ListTile(
              leading: const Icon(Icons.local_fire_department, color: Colors.orange),
              title: const Text('Bombeiros'),
              subtitle: const Text('193'),
              trailing: const Icon(Icons.phone),
              onTap: () => TelefoneService.discar('193'),
            ),
            ListTile(
              leading: const Icon(Icons.local_hospital, color: Colors.green),
              title: const Text('SAMU'),
              subtitle: const Text('192'),
              trailing: const Icon(Icons.phone),
              onTap: () => TelefoneService.discar('192'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Boas Práticas

1. **Sempre solicite permissões** antes de acessar recursos
2. **Verifique se o dispositivo suporta telefonia** (tablets podem não ter)
3. **Trate erros** de forma amigável
4. **Respeite a privacidade** dos contatos
5. **Use ícones claros** para indicar ações de ligação/SMS

---

## Troubleshooting

| Problema                     | Solução                                                       |
| ---------------------------- | ------------------------------------------------------------- |
| "canLaunchUrl" retorna false | Verifique se o esquema está correto (tel:, sms:)              |
| Permissão negada             | Verifique AndroidManifest.xml e solicite em tempo de execução |
| Contatos vazios              | Verifique permissão READ_CONTACTS                             |
| SMS não envia                | Verifique saldo e permissão SEND_SMS                          |

---

## Referências

- **url_launcher:**
  [pub.dev/packages/url_launcher](https://pub.dev/packages/url_launcher)
- **flutter_sms:**
  [pub.dev/packages/flutter_sms](https://pub.dev/packages/flutter_sms)
- **contacts_service:**
  [pub.dev/packages/contacts_service](https://pub.dev/packages/contacts_service)
- **Android Telephony:**
  [developer.android.com/guide/topics/connectivity/telecom](https://developer.android.com/guide/topics/connectivity/telecom)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
