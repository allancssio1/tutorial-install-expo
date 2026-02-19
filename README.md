# Passo a Passo: Configurar React Native com Expo no Windows 11

---

## ETAPA 1 - Instalar o Node.js

1. Acesse **https://nodejs.org/pt-br/download** no navegador  
2. Baixe a versão **LTS** (recomendado – atualmente 20.x ou 22.x)  
3. Execute o instalador `.msi` e siga o wizard:  
   - Marque a opção **"Add to PATH"** (vem marcada por padrão)  
   - Marque **"Automatically install necessary tools"** se aparecer  
4. Após instalar, **feche e reabra o terminal** (PowerShell ou CMD)  
5. Verifique a instalação:

```powershell
node --version
npm --version
```

> **Alternativa (recomendada para devs):** Use o **nvm-windows** para gerenciar versões do Node:
>
> - Baixe em: https://github.com/coreybutler/nvm-windows/releases  
> - Instale, depois rode:
>
> ```powershell
> nvm install lts
> nvm use lts
> ```

---

## ETAPA 2 - Ferramentas de linha de comando do Expo

Hoje não é mais recomendado instalar o `expo-cli` globalmente.  
Use sempre o **CLI via npx**, assim:

- Para criar projeto e rodar comandos, use sempre `npx expo ...` dentro do projeto.  
- Se você for usar builds em nuvem, instale apenas o `eas-cli` globalmente (opcional):

```powershell
npm install -g eas-cli
```

---

## ETAPA 3 - Criar o projeto React Native com Expo

Navegue até a pasta do seu workspace (ajuste o caminho conforme sua máquina):

```powershell
cd C:\Users\SEU_USUARIO\Desktop\work\bcs
```

Crie o projeto:

```powershell
npx create-expo-app@latest nome-do-app
```

O wizard vai perguntar o template.  
Escolha o padrão ou **blank (TypeScript)** para manter consistência com o restante do projeto (que usa TypeScript).

---

## ETAPA 4 - Entrar no projeto

```powershell
cd nome-do-app
```

---

## ETAPA 5 - Instalar dependências

As dependências já são instaladas automaticamente pelo `create-expo-app`, mas se precisar reinstalar:

```powershell
npm install
```

> O projeto existente (`frontend-next`) usa **yarn**. Se preferir manter o padrão:
>
> ```powershell
> npm install -g yarn
> yarn install
> ```

---

## ETAPA 6 - Rodar o projeto

Dentro da pasta do projeto, rode:

```powershell
npx expo start
```

Isso abre o **Metro Bundler** com um QR Code no terminal.  
Você terá as seguintes opções:

| Tecla | Ação                      |
| ----- | ------------------------- |
| `a`   | Abrir no emulador Android |
| `w`   | Abrir no navegador (web)  |
| `r`   | Recarregar o app          |

---

## ETAPA 7 - Testar no celular (opção mais rápida)

1. Instale o app **Expo Go** no celular (Google Play / App Store)  
2. Escaneie o QR Code que aparece no terminal  
3. O app roda direto no celular via Wi‑Fi (celular e PC devem estar na mesma rede)

---

## ETAPA 8 - (Opcional) Configurar emulador Android

Se quiser rodar no emulador em vez do celular:

1. Instale o **Android Studio**: https://developer.android.com/studio  
2. No Android Studio, vá em **More Actions > SDK Manager**:  
   - Instale o **Android SDK** mais recente  
   - Na aba **SDK Tools**, marque **Android Emulator** e **Android SDK Platform-Tools**  
3. Vá em **More Actions > Virtual Device Manager** e crie um dispositivo (ex: Pixel 7, API 34)  
4. Configure a variável de ambiente `ANDROID_HOME`:

```powershell
[System.Environment]::SetEnvironmentVariable("ANDROID_HOME", "$env:LOCALAPPDATA\Android\Sdk", "User")
```

5. Adicione o `platform-tools` ao PATH:

```powershell
[System.Environment]::SetEnvironmentVariable("Path", "$env:Path;$env:LOCALAPPDATA\Android\Sdk\platform-tools", "User")
```

6. **Reinicie o terminal**, depois rode:

```powershell
npx expo start
```

E pressione `a` para abrir no emulador.

---

## Resumo dos comandos (sequência completa)

```powershell
# 1. Verificar Node
node --version

# 2. (Opcional) Instalar EAS CLI globalmente, se precisar de builds
npm install -g eas-cli

# 3. Criar projeto
cd C:\Users\SEU_USUARIO\Desktop\work\bcs
npx create-expo-app@latest nome-do-app

# 4. Entrar e rodar
cd nome-do-app
npx expo start
```

---

## Dicas importantes

- **Firewall:** Se o celular não conectar, verifique se o Windows Firewall não está bloqueando as portas usadas pelo Expo (como 19000/19001).  
- **Mesma rede:** PC e celular DEVEM estar na mesma rede Wi‑Fi para o Expo Go funcionar.  
- **Tunnel mode:** Se tiver problemas de rede, rode `npx expo start --tunnel` (pode instalar o `@expo/ngrok` automaticamente).  
- **TypeScript:** O projeto BCS existente usa TypeScript, então recomendo usar o template TS ao criar o app Expo para manter consistência.
