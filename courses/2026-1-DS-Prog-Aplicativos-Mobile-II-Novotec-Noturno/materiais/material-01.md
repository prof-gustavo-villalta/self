---
layout: material
title: "Material 01 - Guia de Instalação Flutter"
---

## ⚡ Passo a Passo Resumido

### 1. Download Flutter

```
https://storage.googleapis.com/flutter_infra_release/releases/stable/windows/flutter_windows_3.41.5-stable.zip
→ Extrair para: C:\flutter
```

### 2. Configurar Variáveis de Ambiente

```
Painel de Controle → Sistema → Configurações avançadas do sistema
→ Variáveis de Ambiente → Path → Novo
→ Adicionar: C:\flutter\bin
```

### 3. Verificar Instalação

```bash
flutter doctor
```

### 4. Instalar Android Studio

```
https://developer.android.com/studio
→ Instalar com configurações padrão
```

### 5. Configurar Android SDK

```
Android Studio → Configure → SDK Manager
→ SDK Platforms: Android API 34, 33, 28
→ SDK Tools: Todos os itens obrigatórios
```

### 6. Aceitar Licenças

```bash
flutter doctor --android-licenses
→ Digitar 'y' para todas
```

### 7. Instalar VS Code

```
https://code.visualstudio.com
→ Extensões: Flutter e Dart
```

### 8. Criar Emulador

```
Android Studio → Configure → AVD Manager
→ Create Virtual Device → Pixel 7 → API 34
```

### 9. Criar Projeto

```bash
flutter create meu_app
cd meu_app
flutter run
```

---

## 🛠️ Comandos Úteis

| Comando                   | Descrição          |
| ------------------------- | ------------------ |
| `flutter doctor`          | Verifica ambiente  |
| `flutter create nome_app` | Cria novo projeto  |
| `flutter run`             | Executa o app      |
| `flutter devices`         | Lista dispositivos |
| `flutter clean`           | Limpa build        |
| `flutter pub get`         | Baixa dependências |
| `flutter build apk`       | Gera APK           |

---

## 🔧 Troubleshooting

### Problema: "flutter" não é reconhecido

**Solução:** Verificar se `C:\flutter\bin` está no Path

### Problema: Licenças Android pendentes

**Solução:** Executar `flutter doctor --android-licenses`

### Problema: Dispositivo não aparece

**Solução:**

- Verificar depuração USB no celular
- Instalar drivers USB do fabricante
- Verificar cabo USB

### Problema: Emulador lento

**Solução:**

- Ativar Intel HAXM (processadores Intel)
- Aumentar RAM do emulador
- Usar dispositivo físico

---

## 📞 Suporte

Em caso de dúvidas:

1. Consultar documentação oficial: docs.flutter.dev
2. Verificar mensagens do `flutter doctor`
3. Perguntar ao professor
4. Pesquisar em fóruns (Stack Overflow, Flutter Community)

---

**ETEC Ferrucio Humberto Gazzetta - Nova Odessa** **Disciplina:** Programação de
Aplicativos Mobile II **Professor:** Gustavo de Oliveira Villalta
