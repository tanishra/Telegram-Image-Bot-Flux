# 🖼️ Telegram AI Image Generator Bot

A simple yet powerful Telegram bot that generates images from **text** or **voice prompts** using the `black-forest-labs/FLUX.1-schnell` model powered by EURI AI.

Built using:
- [n8n](https://n8n.io) for workflow automation
- [Telegram Bot API](https://core.telegram.org/bots)
- [EURI API](https://euron.one) (or [Hugging Face](https://huggingface.co) as fallback)
- FLUX.1-schnell – an advanced AI model for text-to-image generation

---

## ✨ Features

- 📸 Generate AI images from text or **voice prompts**
- 🎙️ Voice-to-image using automatic speech-to-text
- 🧠 Powered by `black-forest-labs/FLUX.1-schnell` and [EURI API](https://euron.one)
- 🤖 Telegram bot interface
- 🔄 Fully automated with n8n workflows
- 🧪 Easy to deploy, test, and customize

---

## 📷 Live Demo

Try the bot here: [@tanishrajput_bot](https://t.me/tanishrajput_bot)

You can use either:

### 📄 Text prompt:
create an image of BMW car

### 🎙️ Voice prompt:
- Send a **voice note** (e.g., "create an image of a robot painting in a forest")
- Bot will transcribe it and generate an image

---

## 🧰 Tech Stack

- **n8n** – No-code/low-code automation platform
- **Telegram Bot API** – For handling user messages
- **EURI API** – For fast, production-ready AI image generation
- **Hugging Face API** – As an alternative inference source
- **black-forest-labs/FLUX.1-schnell** – Text-to-image generation model

---

## 🛠️ Project Setup

### Clone the Repo

```bash
git clone https://github.com/tanishra/Telegram-Image-Bot-Flux.git
cd Telegram-Image-Bot-Flux
```

1. Import Workflow
Go to your n8n dashboard and import the file:
/workflows/Telegram_Bot.json

This file contains the complete logic to:
- Telegram text messages
- Telegram voice messages
- Prompt extraction (from text or voice)
- Image generation via EURI API
- Sending image back to user

2. Telegram Trigger Node Setup
Configure the Telegram Trigger node:
- Add your Telegram credentials (use the bot token)

3. HTTP Request Node (EURI)
Configure your API request as follows:

Endpoint:
```bash
https://api.euron.one/api/v1/euri/images/generations
```

Headers:
```http
{
  "Content-Type": "application/json",
  "Authorization": "Bearer YOUR_API_TOKEN"
}
````

Body:
```bash
{
  "prompt": "fetch from your telegram node something like {{ $json['message']['text']}}",
  "model": "black-forest-labs/FLUX.1-schnell",
  "n": 1,
  "size": "1024x1024",
  "quality": "standard",
  "response_format": "url",
  "style": "vivid"
}
```

---

## 🌐 API Support
- ✅ EURI API (Recommended)
- Fast, production-ready image generation
- No need to host your own models
- Get your API key at euron.one
- Example cURL Request:

```bash
curl -X POST https://api.euron.one/api/v1/euri/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{
    "prompt": "A beautiful sunset over mountains",
    "model": "black-forest-labs/FLUX.1-schnell",
    "n": 2,
    "size": "1024x1024",
    "quality": "standard",
    "response_format": "url",
    "style": "vivid"
  }'
```

--- 


## 🔧 Contributing

Contributions are welcome!  
If you have ideas, bug fixes, or improvements:

1. Fork the repo  
2. Create a branch (`feature/your-feature`)  
3. Make your changes  
4. Submit a Pull Request

Keep changes focused and documented.  
Let’s build something awesome together!
