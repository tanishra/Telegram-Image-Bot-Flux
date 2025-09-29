# Telegram Bot Setup Instructions

## 1. Create a Telegram Bot

**Step 1: Talk to [@BotFather](https://t.me/BotFather)**  
Send `/start` to @BotFather on Telegram.

**Step 2: Create a New Bot**  
Send:  /newbot

Follow the prompts:
- Choose a name (e.g., `ImageGenBot`)
- Choose a username (must end in `bot`, e.g., `tanishrajput_bot`)

**Step 3: Get Your Bot Token**  
BotFather will return something like:

Use this token to access the HTTP API:
123456789:ABCdefGhIjkLmNoPqRsTuVwXyZ


Save this token. You’ll need it in n8n.

---

## 2. Add Bot Token to n8n

TELEGRAM_BOT_TOKEN=your_bot_token_here

---

## 3. Set Up Telegram Trigger in n8n

In your n8n workflow:

1. **Add "Telegram Trigger" node**
   - Resource: `Message`
   - Operation: `On Message`
   - Update Webhook URL: ✅ Enabled
   - Credentials: Use your bot token
   - Event: `Text`

2. **Optional: Filter messages**  
   Use a Switch node to handle only valid prompt commands (e.g., `/image cat in a spacesuit`).

---

## 4. Send Image Back to User

1. Add an **HTTP Request** node or function to call the FLUX model  
2. Add a **Telegram node → Send Photo**  
   - Chat ID: `={{$json["message"]["chat"]["id"]}}`  
   - Photo: Image URL or binary output  
   - Caption: Optional

---

## 5. Test the Bot

Send a message to your bot like:
create an image of bmw car

It will generate the image using FLUX, and reply in the chat.
