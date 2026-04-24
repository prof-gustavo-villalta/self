---
layout: material
title: "Material 06 - Câmera e Galeria de Imagens"
---

# 📸 Câmera e Galeria de Imagens em Flutter

Guia completo para integrar câmera e acesso à galeria de fotos em aplicativos
Flutter, incluindo preview em tempo real, captura de fotos e seleção de imagens.

---

## Pacotes Necessários

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.10.5+9 # Acesso à câmera
  image_picker: ^1.0.7 # Galeria e câmera simplificada
  path_provider: ^2.1.2 # Caminhos de arquivo
  path: ^1.9.0 # Manipulação de paths
```

Execute:

```bash
flutter pub get
```

---

## Opção 1: Image Picker (Mais Simples)

O `image_picker` é a forma mais fácil de acessar câmera e galeria.

### Configuração Android

No `android/app/src/main/AndroidManifest.xml`:

```xml
<manifest>
    <!-- Permissões -->
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <application ...>
        ...
    </application>
</manifest>
```

### Código Completo

```dart
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

class CameraScreen extends StatefulWidget {
  const CameraScreen({super.key});

  @override
  State<CameraScreen> createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  File? _imagemSelecionada;
  final ImagePicker _picker = ImagePicker();

  // Tirar foto com câmera
  Future<void> _tirarFoto() async {
    try {
      final XFile? foto = await _picker.pickImage(
        source: ImageSource.camera,
        maxWidth: 1920,  // Redimensionar
        maxHeight: 1080,
        imageQuality: 85,  // Qualidade JPEG (0-100)
      );

      if (foto != null) {
        setState(() {
          _imagemSelecionada = File(foto.path);
        });
      }
    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro ao tirar foto: $e')),
      );
    }
  }

  // Selecionar da galeria
  Future<void> _selecionarGaleria() async {
    try {
      final XFile? imagem = await _picker.pickImage(
        source: ImageSource.gallery,
        maxWidth: 1920,
        maxHeight: 1080,
        imageQuality: 85,
      );

      if (imagem != null) {
        setState(() {
          _imagemSelecionada = File(imagem.path);
        });
      }
    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro ao selecionar imagem: $e')),
      );
    }
  }

  // Selecionar múltiplas imagens
  Future<void> _selecionarMultiplas() async {
    try {
      final List<XFile> imagens = await _picker.pickMultiImage(
        maxWidth: 1920,
        maxHeight: 1080,
        imageQuality: 85,
      );

      // imagens contém a lista de arquivos selecionados
      for (var imagem in imagens) {
        print('Imagem: ${imagem.path}');
      }
    } catch (e) {
      print('Erro: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Câmera e Galeria'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // Preview da imagem
            Container(
              width: 300,
              height: 300,
              decoration: BoxDecoration(
                color: Colors.grey[300],
                borderRadius: BorderRadius.circular(12),
              ),
              child: _imagemSelecionada != null
                ? ClipRRect(
                    borderRadius: BorderRadius.circular(12),
                    child: Image.file(
                      _imagemSelecionada!,
                      fit: BoxFit.cover,
                    ),
                  )
                : const Icon(
                    Icons.image,
                    size: 100,
                    color: Colors.grey,
                  ),
            ),
            const SizedBox(height: 32),

            // Botões
            ElevatedButton.icon(
              onPressed: _tirarFoto,
              icon: const Icon(Icons.camera_alt),
              label: const Text('Tirar Foto'),
            ),
            const SizedBox(height: 12),
            ElevatedButton.icon(
              onPressed: _selecionarGaleria,
              icon: const Icon(Icons.photo_library),
              label: const Text('Escolher da Galeria'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Opção 2: Câmera com Preview (Mais Avançada)

Para controle total da câmera com preview em tempo real.

### Inicialização

```dart
import 'package:camera/camera.dart';

late List<CameraDescription> cameras;

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  cameras = await availableCameras();
  runApp(const MyApp());
}
```

### Tela com Preview

```dart
class CameraPreviewScreen extends StatefulWidget {
  const CameraPreviewScreen({super.key});

  @override
  State<CameraPreviewScreen> createState() => _CameraPreviewScreenState();
}

class _CameraPreviewScreenState extends State<CameraPreviewScreen> {
  CameraController? _controller;
  bool _isReady = false;
  bool _isBackCamera = true;

  @override
  void initState() {
    super.initState();
    _initCamera();
  }

  Future<void> _initCamera() async {
    if (cameras.isEmpty) return;

    _controller = CameraController(
      cameras[_isBackCamera ? 0 : 1],  // 0 = traseira, 1 = frontal
      ResolutionPreset.high,
    );

    await _controller!.initialize();

    if (mounted) {
      setState(() => _isReady = true);
    }
  }

  Future<void> _tirarFoto() async {
    if (_controller == null || !_controller!.value.isInitialized) return;

    try {
      final foto = await _controller!.takePicture();

      if (mounted) {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (_) => PreviewScreen(imagePath: foto.path),
          ),
        );
      }
    } catch (e) {
      print('Erro ao tirar foto: $e');
    }
  }

  void _trocarCamera() {
    setState(() {
      _isBackCamera = !_isBackCamera;
      _isReady = false;
    });
    _controller?.dispose();
    _initCamera();
  }

  @override
  void dispose() {
    _controller?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (!_isReady || _controller == null) {
      return const Scaffold(
        body: Center(child: CircularProgressIndicator()),
      );
    }

    return Scaffold(
      body: Stack(
        fit: StackFit.expand,
        children: [
          // Preview da câmera
          CameraPreview(_controller!),

          // Botão de captura
          Positioned(
            bottom: 30,
            left: 0,
            right: 0,
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                // Trocar câmera
                IconButton(
                  icon: const Icon(Icons.flip_camera_ios, color: Colors.white, size: 32),
                  onPressed: _trocarCamera,
                ),

                // Botão de foto
                GestureDetector(
                  onTap: _tirarFoto,
                  child: Container(
                    width: 80,
                    height: 80,
                    decoration: BoxDecoration(
                      shape: BoxShape.circle,
                      border: Border.all(color: Colors.white, width: 4),
                    ),
                    child: Container(
                      margin: const EdgeInsets.all(4),
                      decoration: const BoxDecoration(
                        shape: BoxShape.circle,
                        color: Colors.white,
                      ),
                    ),
                  ),
                ),

                // Espaçamento
                const SizedBox(width: 50),
              ],
            ),
          ),
        ],
      ),
    );
  }
}

// Tela de preview da foto
class PreviewScreen extends StatelessWidget {
  final String imagePath;

  const PreviewScreen({super.key, required this.imagePath});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        fit: StackFit.expand,
        children: [
          Image.file(File(imagePath), fit: BoxFit.cover),
          Positioned(
            bottom: 30,
            left: 0,
            right: 0,
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                IconButton(
                  icon: const Icon(Icons.close, color: Colors.white, size: 40),
                  onPressed: () => Navigator.pop(context),
                ),
                IconButton(
                  icon: const Icon(Icons.check, color: Colors.green, size: 40),
                  onPressed: () {
                    // Salvar ou usar a imagem
                    Navigator.pop(context, imagePath);
                  },
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

---

## Upload de Imagem para Servidor

```dart
import 'dart:io';
import 'package:http/http.dart' as http;
import 'package:http_parser/http_parser.dart';

class UploadService {
  static Future<void> uploadImagem(File imagem, String userId) async {
    try {
      var request = http.MultipartRequest(
        'POST',
        Uri.parse('https://sua-api.com/upload'),
      );

      // Adicionar arquivo
      request.files.add(
        await http.MultipartFile.fromPath(
          'imagem',
          imagem.path,
          contentType: MediaType('image', 'jpeg'),
        ),
      );

      // Adicionar campos
      request.fields['userId'] = userId;

      var response = await request.send();

      if (response.statusCode == 200) {
        print('Upload bem-sucedido!');
      } else {
        print('Erro no upload: ${response.statusCode}');
      }
    } catch (e) {
      print('Erro: $e');
    }
  }
}
```

---

## Permissões em Tempo de Execução

Para Android 6.0+ (API 23+), adicione o pacote `permission_handler`:

```yaml
dependencies:
  permission_handler: ^11.3.0
```

```dart
import 'package:permission_handler/permission_handler.dart';

Future<bool> _solicitarPermissoes() async {
  // Android 13+ (API 33+)
  final photos = await Permission.photos.request();
  final camera = await Permission.camera.request();

  return photos.isGranted && camera.isGranted;
}
```

---

## Boas Práticas

1. **Redimensione imagens** antes de enviar (economiza dados)
2. **Comprima JPEG** com imageQuality 70-85
3. **Verifique permissões** antes de acessar
4. **Libere recursos** com dispose()
5. **Trate erros** de forma amigável

---

## Referências

- **image_picker**:
  [pub.dev/packages/image_picker](https://pub.dev/packages/image_picker)
- **camera**: [pub.dev/packages/camera](https://pub.dev/packages/camera)
- **permission_handler**:
  [pub.dev/packages/permission_handler](https://pub.dev/packages/permission_handler)
- \*\*Flutter Cookbook - Images](https://docs.flutter.dev/cookbook/images)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
