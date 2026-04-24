# AI Call Shield

AI Call Shield is a final year project built to protect elderly users from phone scams. It intercepts calls before they reach the recipient, runs the caller through an AI-powered screening conversation, and presents the recipient with a verdict so they can decide whether to answer.

## What It Does

When someone calls, the system asks them a series of questions. The caller's answers are transcribed and analysed by an AI model (GPT-4o) which looks for signs of fraud — pressure tactics, impersonation, requests for money or personal data, and other common scam patterns. The recipient sees the result and chooses to accept or block the call.

Recipients can personalise the screening by providing their name, age, and country. The AI uses this to detect tactics targeted specifically at them. Trusted contacts skip screening entirely.

## Components

The project has three parts that work together:

- **Server** — A Node.js backend that handles call routing, runs the AI screening, and connects the two devices.
- **CallerApp** — An Android app for the person placing the call. It drives the screening conversation.
- **CallScreen** — An Android app for the person receiving the call. It displays the AI verdict and records their decision.

## Tech Stack

Node.js, Express, WebSocket, OpenAI API (GPT-4o + Whisper), Kotlin, Android SDK, WebRTC.

## Setup

See [setup.md](./setup.md) for installation and configuration instructions.
