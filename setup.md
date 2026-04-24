# AI Call Screen — Setup Documentation

This document covers how to set up the Node.js server, the CallerApp (Android), and the CallScreen (Android) so all three components can communicate.

---

## Prerequisites

- **Node.js** v18 or higher
- **npm** v9 or higher
- **Android Studio** (Hedgehog or later)
- **Android device or emulator** running API 26 (Android 8.0) or higher
- An **OpenAI API key** with access to GPT-4o and Whisper

---

## 1. Server

The server is the central hub. Start it before launching either Android app.

**Install dependencies:**
```bash
cd Code/server
npm install
```

**Configure environment:**
```bash
cp .env.example .env
```

Open `.env` and fill in your values:
```
OPENAI_API_KEY=sk-your-key-here
PORT=3000
CLASSIFICATION_MODEL=gpt-4o
SCREENING_DURATION=15
```

**Run the server:**
```bash
node server.js
```

The server listens on `http://localhost:3000` by default. Confirm it is running by visiting `http://localhost:3000/api/health` in a browser. You should receive a JSON status response.

**Note:** Both Android devices must be able to reach the server over the network. If testing on physical devices, the server must be reachable via your local IP address (e.g. `192.168.1.x`), not `localhost`.

---

## 2. CallerApp (Android)

This app runs on the device that places the call. It handles AI screening and WebRTC audio.

**Open the project:**
1. Open Android Studio.
2. Select **File > Open** and navigate to `Code/CallerApp`.
3. Let Gradle sync finish.

**Build and run:**
- Connect your Android device via USB or start an emulator.
- Press **Run** (Shift+F10).

**Configure at launch:**
- Enter a **User ID** for the caller (any unique string, e.g. `caller1`).
- Enter the **server address** (IP or hostname of the machine running the server).
- Enter the **server port** (default `3000`).
- Enter the **target User ID** of the receiver you want to call.
- Press **Connect**, then **Call** to initiate a call.

Grant microphone permission when prompted.

---

## 3. CallScreen (Android)

This app runs on the device that receives the call. It displays the AI screening verdict and lets the user accept or reject.

**Open the project:**
1. Open Android Studio.
2. Select **File > Open** and navigate to `Code/CallScreen`.
3. Let Gradle sync finish.

**Build and run:**
- Connect a second Android device or start a second emulator.
- Press **Run**.

**Configure at launch:**
- Enter a **User ID** for the receiver (e.g. `receiver1`).
- Enter the same **server address** and **port** used by the CallerApp.
- Press **Connect** to register with the server and wait for incoming calls.

---

## End-to-End Test

1. Start the server.
2. Launch CallScreen on the receiver device. Connect with a user ID (e.g. `receiver1`).
3. Launch CallerApp on the caller device. Connect and set the target to `receiver1`.
4. Press **Call**. The AI screening flow will begin automatically.
5. The receiver sees the screening verdict and can accept or reject the call.
