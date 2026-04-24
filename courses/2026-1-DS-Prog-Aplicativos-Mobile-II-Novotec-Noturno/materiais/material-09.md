---
layout: material
title: "Material 09 - WebSocket e Comunicação em Tempo Real"
---

# 🔌 WebSocket e Comunicação em Tempo Real

Guia completo sobre comunicação bidirecional em tempo real usando WebSockets em
Flutter, incluindo chat ao vivo, notificações instantâneas e broadcast de dados.

---

## HTTP vs WebSocket

| Característica  | HTTP                             | WebSocket                 |
| --------------- | -------------------------------- | ------------------------- |
| **Comunicação** | Unidirecional (request/response) | Bidirecional              |
| **Conexão**     | Nova a cada requisição           | Conexão persistente       |
| **Overhead**    | Alto (headers em cada request)   | Baixo (após handshake)    |
| **Tempo real**  | Não (polling necessário)         | Sim, nativo               |
| **Uso ideal**   | Dados estáticos, APIs REST       | Chat, notificações, jogos |

### Analogia

- **HTTP:** Como enviar cartas pelo correio (cada mensagem é independente)
- **WebSocket:** Como uma ligação telefônica (conexão aberta, fala em tempo
  real)

---

## Configuração

### Dependências

```yaml
dependencies:
  flutter:
    sdk: flutter
  web_socket_channel: ^2.4.5
```

Execute:

```bash
flutter pub get
```

### Permissões Android

No `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

---

## Implementação Completa

### 1. Service WebSocket

```dart
import 'dart:async';
import 'dart:convert';
import 'package:web_socket_channel/web_socket_channel.dart';
import 'package:web_socket_channel/io.dart';

class WebSocketService {
  WebSocketChannel? _channel;
  final _messageController = StreamController<Map<String, dynamic>>.broadcast();
  final _connectionController = StreamController<bool>.broadcast();

  bool _isConnected = false;

  // Stream para ouvir mensagens
  Stream<Map<String, dynamic>> get messageStream => _messageController.stream;
  Stream<bool> get connectionStream => _connectionController.stream;
  bool get isConnected => _isConnected;

  // Conectar ao servidor
  Future<void> connect(String url) async {
    try {
      _channel = IOWebSocketChannel.connect(url);
      _isConnected = true;
      _connectionController.add(true);

      // Ouvir mensagens recebidas
      _channel!.stream.listen(
        (message) {
          try {
            final data = json.decode(message);
            _messageController.add(data);
          } catch (e) {
            print('Erro ao decodificar mensagem: $e');
          }
        },
        onError: (error) {
          print('Erro na conexão: $error');
          _disconnect();
        },
        onDone: () {
          print('Conexão fechada');
          _disconnect();
        },
      );
    } catch (e) {
      print('Erro ao conectar: $e');
      _disconnect();
    }
  }

  // Enviar mensagem
  void sendMessage(Map<String, dynamic> data) {
    if (_isConnected && _channel != null) {
      _channel!.sink.add(json.encode(data));
    } else {
      print('WebSocket não está conectado');
    }
  }

  // Desconectar
  void disconnect() {
    _disconnect();
  }

  void _disconnect() {
    _isConnected = false;
    _connectionController.add(false);
    _channel?.sink.close();
    _channel = null;
  }

  void dispose() {
    _disconnect();
    _messageController.close();
    _connectionController.close();
  }
}
```

### 2. Modelo de Mensagem

```dart
class ChatMessage {
  final String id;
  final String sender;
  final String content;
  final DateTime timestamp;
  final bool isMe;

  ChatMessage({
    required this.id,
    required this.sender,
    required this.content,
    required this.timestamp,
    this.isMe = false,
  });

  factory ChatMessage.fromJson(Map<String, dynamic> json) {
    return ChatMessage(
      id: json['id'] ?? DateTime.now().millisecondsSinceEpoch.toString(),
      sender: json['sender'] ?? 'Desconhecido',
      content: json['content'] ?? '',
      timestamp: json['timestamp'] != null
          ? DateTime.parse(json['timestamp'])
          : DateTime.now(),
      isMe: json['isMe'] ?? false,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'sender': sender,
      'content': content,
      'timestamp': timestamp.toIso8601String(),
    };
  }
}
```

### 3. Tela de Chat Completa

```dart
import 'package:flutter/material.dart';
import 'dart:math';
import '../models/chat_message.dart';
import '../services/websocket_service.dart';

class ChatScreen extends StatefulWidget {
  final String username;

  const ChatScreen({super.key, required this.username});

  @override
  State<ChatScreen> createState() => _ChatScreenState();
}

class _ChatScreenState extends State<ChatScreen> {
  final WebSocketService _webSocketService = WebSocketService();
  final TextEditingController _messageController = TextEditingController();
  final ScrollController _scrollController = ScrollController();
  final List<ChatMessage> _messages = [];
  bool _isConnected = false;

  // URL do servidor WebSocket (exemplo)
  final String _wsUrl = 'wss://echo.websocket.org/';

  @override
  void initState() {
    super.initState();
    _connect();
  }

  Future<void> _connect() async {
    await _webSocketService.connect(_wsUrl);

    _webSocketService.connectionStream.listen((connected) {
      setState(() => _isConnected = connected);

      if (connected) {
        _addSystemMessage('Conectado ao chat!');
      } else {
        _addSystemMessage('Desconectado. Tentando reconectar...');
      }
    });

    _webSocketService.messageStream.listen((data) {
      setState(() {
        _messages.add(ChatMessage.fromJson(data));
      });
      _scrollToBottom();
    });
  }

  void _addSystemMessage(String text) {
    setState(() {
      _messages.add(ChatMessage(
        id: DateTime.now().millisecondsSinceEpoch.toString(),
        sender: 'Sistema',
        content: text,
        timestamp: DateTime.now(),
      ));
    });
  }

  void _sendMessage() {
    final text = _messageController.text.trim();
    if (text.isEmpty) return;

    final message = ChatMessage(
      id: DateTime.now().millisecondsSinceEpoch.toString(),
      sender: widget.username,
      content: text,
      timestamp: DateTime.now(),
      isMe: true,
    );

    // Enviar via WebSocket
    _webSocketService.sendMessage(message.toJson());

    // Adicionar na lista local
    setState(() {
      _messages.add(message);
      _messageController.clear();
    });

    _scrollToBottom();
  }

  void _scrollToBottom() {
    Future.delayed(const Duration(milliseconds: 100), () {
      if (_scrollController.hasClients) {
        _scrollController.animateTo(
          _scrollController.position.maxScrollExtent,
          duration: const Duration(milliseconds: 300),
          curve: Curves.easeOut,
        );
      }
    });
  }

  @override
  void dispose() {
    _webSocketService.dispose();
    _messageController.dispose();
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text('Chat em Tempo Real'),
            Text(
              _isConnected ? '● Online' : '● Offline',
              style: TextStyle(
                fontSize: 12,
                color: _isConnected ? Colors.green : Colors.red,
              ),
            ),
          ],
        ),
        actions: [
          IconButton(
            icon: Icon(_isConnected ? Icons.link : Icons.link_off),
            onPressed: _isConnected
              ? () => _webSocketService.disconnect()
              : _connect,
          ),
        ],
      ),
      body: Column(
        children: [
          // Lista de mensagens
          Expanded(
            child: _messages.isEmpty
              ? const Center(
                  child: Text(
                    'Nenhuma mensagem ainda\nComece a conversar!',
                    textAlign: TextAlign.center,
                  ),
                )
              : ListView.builder(
                  controller: _scrollController,
                  padding: const EdgeInsets.all(8),
                  itemCount: _messages.length,
                  itemBuilder: (context, index) {
                    return _buildMessageBubble(_messages[index]);
                  },
                ),
          ),

          // Campo de entrada
          Container(
            padding: const EdgeInsets.all(8),
            decoration: BoxDecoration(
              color: Colors.grey[100],
              border: Border(top: BorderSide(color: Colors.grey[300]!)),
            ),
            child: Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: _messageController,
                    decoration: const InputDecoration(
                      hintText: 'Digite sua mensagem...',
                      border: OutlineInputBorder(),
                      contentPadding: EdgeInsets.symmetric(
                        horizontal: 16,
                        vertical: 12,
                      ),
                    ),
                    onSubmitted: (_) => _sendMessage(),
                  ),
                ),
                const SizedBox(width: 8),
                FloatingActionButton(
                  mini: true,
                  onPressed: _isConnected ? _sendMessage : null,
                  child: const Icon(Icons.send),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildMessageBubble(ChatMessage message) {
    final isMe = message.isMe || message.sender == widget.username;
    final isSystem = message.sender == 'Sistema';

    if (isSystem) {
      return Center(
        child: Container(
          margin: const EdgeInsets.symmetric(vertical: 8),
          padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 6),
          decoration: BoxDecoration(
            color: Colors.grey[300],
            borderRadius: BorderRadius.circular(12),
          ),
          child: Text(
            message.content,
            style: const TextStyle(fontSize: 12, color: Colors.black54),
          ),
        ),
      );
    }

    return Align(
      alignment: isMe ? Alignment.centerRight : Alignment.centerLeft,
      child: Container(
        margin: const EdgeInsets.symmetric(vertical: 4, horizontal: 8),
        padding: const EdgeInsets.all(12),
        constraints: BoxConstraints(
          maxWidth: MediaQuery.of(context).size.width * 0.75,
        ),
        decoration: BoxDecoration(
          color: isMe ? Colors.blue[100] : Colors.grey[200],
          borderRadius: BorderRadius.only(
            topLeft: const Radius.circular(16),
            topRight: const Radius.circular(16),
            bottomLeft: Radius.circular(isMe ? 16 : 4),
            bottomRight: Radius.circular(isMe ? 4 : 16),
          ),
        ),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            if (!isMe)
              Text(
                message.sender,
                style: const TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 12,
                  color: Colors.blue,
                ),
              ),
            Text(message.content),
            const SizedBox(height: 4),
            Text(
              '${message.timestamp.hour.toString().padLeft(2, '0')}:${message.timestamp.minute.toString().padLeft(2, '0')}',
              style: TextStyle(
                fontSize: 10,
                color: Colors.grey[600],
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

## Servidores WebSocket para Teste

| Servidor           | URL                               | Descrição                 |
| ------------------ | --------------------------------- | ------------------------- |
| WebSocket.org Echo | `wss://echo.websocket.org/`       | Ecoa mensagens de volta   |
| Postman            | `wss://ws.postman-echo.com/raw`   | Servidor de teste Postman |
| PieSocket          | `wss://demo.piesocket.com/v3/...` | Cluster gratuito          |

---

## Casos de Uso em Apps Mobile

### 1. Notificações em Tempo Real

```dart
// Exemplo: Receber notificação de novo pedido
_webSocketService.messageStream.listen((data) {
  if (data['type'] == 'new_order') {
    showDialog(
      context: context,
      builder: (_) => AlertDialog(
        title: const Text('Novo Pedido!'),
        content: Text('Pedido #${data['orderId']} recebido'),
      ),
    );
  }
});
```

### 2. Atualização de Dados em Tempo Real

```dart
// Exemplo: Painel de vendas ao vivo
_webSocketService.messageStream.listen((data) {
  if (data['type'] == 'sales_update') {
    setState(() {
      _todaySales = data['total'];
      _salesChart.add(data['chart_point']);
    });
  }
});
```

### 3. Indicador de "Digitando..."

```dart
// Enviar status
void _onTyping() {
  _webSocketService.sendMessage({
    'type': 'typing',
    'user': widget.username,
    'isTyping': _messageController.text.isNotEmpty,
  });
}

// Receber status
_webSocketService.messageStream.listen((data) {
  if (data['type'] == 'typing') {
    setState(() {
      _typingUsers = data['users'];
    });
  }
});
```

---

## Boas Práticas

1. **Reconexão automática:** Implemente retry com backoff exponencial
2. **Heartbeat:** Envie pings periódicos para manter conexão
3. **Compressão:** Use compressão para dados grandes
4. **Autenticação:** Envie token na URL ou no primeiro handshake
5. **Tratamento de erro:** Sempre tenha fallback para HTTP polling

---

## Troubleshooting

| Problema             | Solução                            |
| -------------------- | ---------------------------------- |
| Conexão recusada     | Verifique URL e porta              |
| Timeout              | Verifique firewall e proxy         |
| Desconexão frequente | Implemente heartbeat               |
| Mensagens duplicadas | Adicione ID único em cada mensagem |

---

## Referências

- **web_socket_channel:**
  [pub.dev/packages/web_socket_channel](https://pub.dev/packages/web_socket_channel)
- **WebSockets MDN:**
  [developer.mozilla.org/Web/API/WebSockets_API](https://developer.mozilla.org/pt-BR/docs/Web/API/WebSockets_API)
- **Socket.IO:** [socket.io](https://socket.io/) (alternativa popular)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
