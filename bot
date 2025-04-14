import asyncio
import aiohttp
from aiogram import Bot
import os

bot = Bot(token=os.getenv("TELEGRAM_TOKEN"))
CHANNEL_ID = os.getenv("CHANNEL_ID")
FASTGPT_API_KEY = os.getenv("FASTGPT_API_KEY")

async def get_prediction():
    url = "https://api.fastgpt.run/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {FASTGPT_API_KEY}",
        "Content-Type": "application/json"
    }
    data = {
        "model": "gpt-3.5-turbo",
        "messages": [
            {"role": "user", "content": "Дай прогнозы и главные новости спорта на сегодня."}
        ]
    }

    async with aiohttp.ClientSession() as session:
        async with session.post(url, headers=headers, json=data) as resp:
            response = await resp.json()
            return response["choices"][0]["message"]["content"]

async def main():
    result = await get_prediction()
    await bot.send_message(CHANNEL_ID, result)

if __name__ == "__main__":
    asyncio.run(main())
