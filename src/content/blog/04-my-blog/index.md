---
title: "Setting up dev environment for react native on Windows"
description: ""
date: "April 17 2026"
---

## Step 1: Install Node.js

Download and install from [nodejs.org](https://nodejs.org). Verify the installation:

```bash
node -v
npm -v
```

---

## Step 2: Install a Code Editor

Download VS Code from [code.visualstudio.com](https://code.visualstudio.com). Any other editor is also supported.

---

## Step 3: Install Chocolatey

Open PowerShell as Administrator and run:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

---

## Step 4: Install JDK and Node via Chocolatey

```powershell
choco install -y nodejs-lts microsoft-openjdk17
```

Verify the Java installation:

```bash
java -version
```

---

## Step 5: Install Android Studio

Download from [developer.android.com/studio](https://developer.android.com/studio).

During installation, ensure the following components are selected:

- Android SDK

- Android SDK Platform

- Android Virtual Device

Follow the standard installation prompts to complete setup.

---

## Step 6: Configure Environment Variables

1.  Open **Environment Variables** by searching `env` in the Windows search bar.

2.  Under **User Variables**, create a new variable:

    - **Variable name:** `ANDROID_HOME`

    - **Variable value:** `C:\Users\%USERNAME%\AppData\Local\Android\Sdk`

3.  Under **User Variables**, select **Path** → **Edit** → **New**, and add:

    ```plaintext
    C:\Users\%USERNAME%\AppData\Local\Android\Sdk\platform-tools
    ```

4.  Click **OK** to save.

### Verify Environment Variables

Open PowerShell and run the following to confirm `ANDROID_HOME` was created:

```powershell
Get-ChildItem -Path Env:
```

Open Command Prompt and run the following to confirm all tools are installed:

```cmd
node -v
java -version
adb --version
```

---

## Step 7: Configure Android Studio

1.  Go to **File → Settings → Languages & Frameworks → Android SDK**.

2.  Under **SDK Platforms**, install the desired Android version. Example: **Android 15.0 "VanillaIceCream" (API 35)**.

3.  Under **SDK Tools**, install the following:

    - Android SDK Build-Tools

    - Android SDK Command-Line Tools

    - Android Emulator

    - Android Emulator Hypervisor Driver (Installer)

    - Android SDK Platform-Tools

    - Google Play Licensing Library

---

## Step 8: Set Up a Device

In Android Studio, select the **Device Manager** icon (top-right toolbar). Either:

- Create and launch a **virtual device (emulator)**, or

- Connect a physical device via **wireless debugging**.

---

## Step 9: Run Your React Native App

Once a device is active, start your app with:

```bash
npm run android
```

The app will build and launch on the connected emulator or physical device.
