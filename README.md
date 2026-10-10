<div align="center">

<img src="assets/icon.png" alt="Offline AI Assistant" width="120" />

# Offline AI Assistant

**Your private AI companion — fully offline.**

Gemma 4 · Qwen 3.5 · on-device inference · no internet, no account, no cloud.

[![Platform](https://img.shields.io/badge/platform-Android%20%7C%20iOS-3DDC84?logo=android&logoColor=white)](#download)
[![Flutter](https://img.shields.io/badge/Flutter-3.47+-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Offline](https://img.shields.io/badge/network-100%25%20offline-success)](#-100-offline-100-private)
[![Privacy](https://img.shields.io/badge/data-stays%20on%20device-9cf)](#-privacy-by-design)
[![Languages](https://img.shields.io/badge/i18n-11%20languages-orange)](#supported-languages)

**[Download](https://191005.xyz/localai/)** ·
**[Website](https://191005.xyz/localai/)** ·
**[Report an issue](https://github.com/nesror/Offline-AI-Assistant/issues)** ·
**[中文文档](README-CN.md)**

</div>

---

## Why Offline AI Assistant

Natural disasters, remote expeditions, and everyday emergencies share one thing in common: **connectivity fails exactly when you need it most.**

Offline AI Assistant puts a capable large language model directly on your phone. Ask questions, get calm step-by-step guidance, analyze a photo, or run your own local API — with **no Wi-Fi, no mobile data, and no cloud**. Every conversation stays on your device.

> An offline emergency & privacy AI companion supporting the latest local models — including **Gemma 4** and **Qwen 3.5**. Reliable anywhere, truly private.

---

## Highlights

### 📡 100% offline, 100% private
- Fully functional in **airplane mode** — no network required at any point.
- **Private by design**: all inference runs on-device. No account, no sign-up, no telemetry.
- We collect nothing and share nothing. Your chats never leave your phone.
- **Privacy Mode** can keep a conversation entirely in memory, leaving no history behind.

### 🧠 Latest local models, on-device
- **Gemma 4** — Google's flagship open model, fast and capable, with **image understanding**.
- **Qwen 3.5** — compact and quick for everyday questions.
- Import your own **`.litertlm`** models at any time.
- Use **system AI** where available (Gemini Nano on Android, Apple Foundation Models on iOS).
- Switch models anytime to balance speed, quality, and battery.

### 🚑 Emergency & survival knowledge base
12 expert-crafted scenarios across urban disasters, extreme weather, and wilderness survival. Tap a scenario for calm, actionable, step-by-step guidance — even with zero signal. *(See the [full list](#emergency--survival-scenarios).)*

### ⚡ Instant, natural Q&A
Just ask. *"How do I treat a sprained ankle?"* or *"How can I filter water in the wild?"* gets immediate, practical answers tuned for real situations — with streaming replies that appear as they are generated.

### 🖼️ Multimodal — see it, not just read it
Attach a photo and ask about it: read a document, identify an object, or get advice from an image. On-device and offline.

### 🛠️ Your own local AI server
Turn your phone into a private AI endpoint. The built-in **OpenAI-compatible HTTP server** lets tools like ChatBox or Open WebUI use your local model over your own Wi-Fi — no cloud, no API keys, no cost. *(See the [API examples](#openai-compatible-api).)*

### 🌍 Built for real life
- **11 languages** out of the box.
- Model downloads with **resume** and **integrity verification**.
- Fast streaming responses; dark and light themes.
- Works on a plane, off-grid, or whenever you simply don't want to be tracked.

---

## Supported Models

| Model | Where it runs | Highlights |
|-------|---------------|------------|
| **Gemma 4 (E2B)** | On-device download | Flagship on-device model · multimodal image input |
| **Qwen 3.5** | On-device download | Compact, fast everyday chat |
| **Built-in model** | Ships with the app | Instant start, zero-download setup |
| **System AI** | Android / iOS | Gemini Nano (Android), Apple Foundation Models (iOS) |
| **Custom `.litertlm`** | Import from file | Bring your own model |

> Some distribution channels ship without a bundled model to keep the download small — the app then offers a one-tap download on first launch.

---

## Emergency & Survival Scenarios

| Category | Scenarios |
|----------|-----------|
| 🏙️ **Urban Emergency Response** | Residential Fire · Earthquake Safety · Citywide Blackout · Building Collapse |
| 🌪️ **Extreme Weather** | Flash Flood Response · Trapped in a Blizzard · Heatwave Readiness · Typhoon Preparedness |
| 🏕️ **Wilderness Survival** | Lost in the Desert · Stranded on an Island · Injured in the Mountains · Lost & Disoriented |

The **Wilderness Survival** pack unlocks with a one-time purchase — no subscription.

---

## Download

| Platform | Get it |
|----------|--------|
| 🤖 **Android** | [Official download page](https://191005.xyz/localai/) · Google Play |
| 🍎 **iOS** | [Official download page](https://191005.xyz/localai/) · App Store |

Additional mirrors and backup links are available on the [official download page](https://191005.xyz/localai/).

**Requirements**

- Android 11+ (API 30) on a 64-bit ARM device
- iOS 16.0 or later

The first launch may download a model depending on your build. After that, the app works entirely offline.

---

## OpenAI-Compatible API

A built-in HTTP service lets any OpenAI-compatible client use your local model. The default endpoint is:

```
http://<device-ip>:8080/v1/chat/completions
```

Start the server from the in-app settings, then call it from another device on the same Wi-Fi.

### 1. cURL — non-streaming

```bash
curl http://<device-ip>:8080/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "gemma",
        "messages": [
            {"role": "system", "content": "You are an emergency rescue assistant."},
            {"role": "user", "content": "How do I check if a building is safe after an earthquake?"}
        ]
    }'
```

### 2. cURL — streaming

```bash
curl http://<device-ip>:8080/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "gemma",
        "stream": true,
        "messages": [
            {"role": "user", "content": "Hello"}
        ]
    }'
```

### 3. OpenAI SDK (Node.js)

```javascript
import OpenAI from "openai";

const client = new OpenAI({
    apiKey: "local", // No validation for the local service — placeholder only.
    baseURL: "http://<device-ip>:8080/v1",
});

const completion = await client.chat.completions.create({
    model: "gemma",
    messages: [
        { role: "user", content: "How do I purify drinking water during a flood?" },
    ],
});

console.log(completion.choices[0].message.content);
```

### Notes

- Replace `<device-ip>` with your device's actual IP address.
- Streaming vs. non-streaming is controlled by the `stream: true` parameter.
- No real API key is needed — any placeholder works for the local service.
- Point clients such as **ChatBox** or **Open WebUI** at the same base URL to use your phone as their model backend.

---

## Supported Languages

The interface is available in **11 languages**:

| | | | |
|---|---|---|---|
| English | 简体中文 | 日本語 | 한국어 |
| Deutsch | Français | Русский | Español |
| हिन्दी | العربية | Português | |

---

## FAQ

**Does it really work offline?**
Yes. Once a model is on your device, inference runs entirely on-device. No Wi-Fi or mobile data is required — airplane mode works.

**Do I need an account?**
No. There is no sign-up, no login, and no tracking of any kind.

**Which models can I use?**
Gemma 4, Qwen 3.5, a built-in model, system AI where available, and any custom `.litertlm` model you import.

**Where are my conversations stored?**
On your device only (local database). Use **Privacy Mode** to keep a conversation in memory with no history saved.

**Can other apps use my phone's model?**
Yes. Enable the OpenAI-compatible server and point any compatible client at `http://<device-ip>:8080/v1` on the same network.

**The model failed to load — what do I do?**
Open **Settings**, re-install the model, and export the logs for support. Switching the compute backend (CPU/GPU) can also help on some devices.

---

## Reporting Issues & Feedback

This repository is the public home for documentation and issue tracking.

- 🐛 **Found a bug or have a question?** [Open an issue](https://github.com/nesror/Offline-AI-Assistant/issues).
- ✨ **Feature requests** are welcome — please describe the use case.
- When reporting a problem, include your **app version**, **device model**, **OS version**, the **model in use**, and any **exported logs** from the app settings. This makes issues far quicker to resolve.

---

## Disclaimer

Offline AI Assistant provides **informational guidance only** and is not a substitute for professional emergency, medical, or rescue services. In a real emergency, always contact local authorities and trained professionals first.

---

## About

The application itself is proprietary software. This repository hosts public documentation, API examples, and the issue tracker — the application source code is not published here.

<div align="center">

**[Download](https://191005.xyz/localai/)** · **[Website](https://191005.xyz/localai/)** · **[Issues](https://github.com/nesror/Offline-AI-Assistant/issues)** · **[中文文档](README-CN.md)**

<sub>No subscription. No cloud. No compromise.</sub>

</div>
