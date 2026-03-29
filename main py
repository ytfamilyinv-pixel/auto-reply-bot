import os
import telebot
import asyncio
from fastapi import FastAPI, Request

app = FastAPI()

TOKEN = os.getenv("BOT_TOKEN")

if not TOKEN:
    raise ValueError("BOT_TOKEN is missing")

bot = telebot.TeleBot(TOKEN)

@app.get("/")
async def root():
    return {"status": "Bot running"}

@app.post("/webhook")
async def webhook(request: Request):
    data = await request.json()

    if "message" in data:
        msg = data["message"]
        chat_id = msg["chat"]["id"]
        text = msg.get("text", "").lower()

        if text == "/start":
            await asyncio.to_thread(
                bot.send_message, chat_id, "Hello from Railway 🚀"
            )

    return {"ok": True}
