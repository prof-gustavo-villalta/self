---
layout: material
title: "Material 03 - Guia de Instalação Portátil"
---

# 📦 Guia de Instalação Portátil (Sem Admin)

Este guia foi criado especialmente para alunos que utilizam computadores de
laboratório (ETEC) ou máquinas onde não possuem privilégios de administrador.
Vamos aprender a configurar o ambiente Flutter utilizando apenas versões
portáteis.

---

## 1. Organização das Pastas

Como você não tem permissão para instalar na pasta `C:\Program Files`, vamos
criar nosso próprio ambiente dentro do seu perfil de usuário ou em uma unidade
de dados (como o `D:\`).

**Sugestão de estrutura:**

- `C:\Users\SEU_USUARIO\dev\`
  - `\flutter` (Onde ficará o SDK)
  - `\jdk` (Onde ficará o Java)
  - `\android-studio` (A IDE)
  - `\android-sdk` (Os componentes do Android)

---

## 2. Downloads Necessários (Versões .ZIP)

Baixe os arquivos oficiais abaixo. Escolha sempre a opção `.zip` ou
`No-installer`.

1.  **Flutter SDK (3.41.5 Stable)**:
    [Link Direto (.zip)](https://storage.googleapis.com/flutter_infra_release/releases/stable/windows/flutter_windows_3.41.5-stable.zip)
2.  **Java JDK (Temurin 17)**:
    [Página de Downloads Adoptium](https://adoptium.net/temurin/releases/?version=17&os=windows&arch=x64&package=jdk)
    (Selecione a opção `.zip`).
3.  **Android Studio (No-installer)**:
    [Página oficial do Android Studio](https://developer.android.com/studio#downloads)
    (Role até a seção "Binary releases" e baixe o "Windows (64-bit) zip").
4.  **VS Code Portable**:
    [Download VS Code Windows ZIP](https://code.visualstudio.com/sha/download?build=stable&os=win32-x64-archive)
    (Link direto para a versão 64-bit .zip).

---

## 3. Ativando o Modo Portátil no VS Code

O VS Code não é portátil por padrão apenas extraindo o ZIP. Você precisa ativar
o "Portable Mode" para que suas extensões (como a do Flutter) fiquem guardadas
na pasta do programa:

1.  Extraia o arquivo `.zip` do VS Code em uma pasta (ex:
    `C:\Users\SEU_USUARIO\dev\vscode`).
2.  Abra a pasta onde está o arquivo `Code.exe`.
3.  **Crie uma nova pasta chamada `data`** dentro dessa pasta.
4.  Pronto! Agora, ao abrir o `Code.exe`, todas as suas configurações e
    extensões instaladas serão salvas dentro dessa pasta `data`. Você pode até
    copiar essa pasta inteira para um pendrive e levar para casa.

---

## 4. Configurando as Variáveis de Ambiente (Sem Admin)

O Windows permite que você edite variáveis para o seu **próprio usuário** sem
ser admin:

1.  Pressione `Win + R`, digite
    `rundll32.exe sysdm.cpl,EditEnvironmentVariables` e dê **Enter**.
2.  Na lista de cima (**Variáveis de usuário para...**):
    - Procure por **Path**, selecione e clique em **Editar**.
    - Adicione o caminho da pasta bin do Flutter:
      `C:\Users\SEU_USUARIO\dev\flutter\bin`
    - Adicione o caminho da pasta bin do JDK: `C:\Users\SEU_USUARIO\dev\jdk\bin`
    - Clique em OK.
3.  Clique em **Novo** (também nas variáveis de usuário):
    - Nome: `JAVA_HOME`
    - Valor: `C:\Users\SEU_USUARIO\dev\jdk` (Caminho da pasta raiz do Java).

---

## 4. Configuração Final via Terminal

Abra o **PowerShell** ou **Terminal** e execute estes comandos para avisar ao
Flutter onde estão as ferramentas:

```powershell
# Informe onde está o Java
flutter config --jdk-dir "C:\Users\SEU_USUARIO\dev\jdk"

# Informe onde você vai baixar o Android SDK (pode ser dentro do Android Studio ou pasta separada)
flutter config --android-sdk "C:\Users\SEU_USUARIO\dev\android-sdk"
```

---

## 5. Aceitando as Licenças

Para que o Flutter possa compilar seus apps, você precisa aceitar as licenças do
Android:

```powershell
flutter doctor --android-licenses
```

_(Digite `y` e dê Enter para todas as perguntas)._

---

## ⚠️ Dica de Ouro: Use Celular Físico

Em computadores sem Admin, **não é recomendado usar emuladores**, pois eles
exigem drivers de sistema que só admins instalam.

**O que fazer?**

1.  Pegue seu celular Android.
2.  Ative o **Modo Desenvolvedor** e a **Depuração USB**.
3.  Conecte ao computador via cabo.
4.  O Flutter o reconhecerá automaticamente sem exigir permissões de sistema no
    PC.

---

## 🏁 Validando tudo

Execute o comando final para ver se está tudo certo:

```powershell
flutter doctor
```

---

**Material elaborado para o curso de Mobile II - 2026**  
Prof. Gustavo Villalta
