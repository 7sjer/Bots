import asyncio
import logging
from aiogram import Bot, Dispatcher, types
from aiogram.filters import CommandStart

# 1. Setup logging so you can see errors in the console
logging.basicConfig(level=logging.INFO)

TOKEN = "8627761141:AAHdSXjeruFRdQPg8AdSOK_o-L0EdZT0DoM"

bot = Bot(token=TOKEN)
dp = Dispatcher()

# 2. Corrected the type hint and the decorator
@dp.message(CommandStart())
async def start(msg: types.Message):
    await msg.answer(text="Hello")

async def main() -> None:
    # 3. Delete webhook to ensure the bot starts fresh
    await bot.delete_webhook(drop_pending_updates=True)
    await dp.start_polling(bot)

if __name__ == "__main__":
    try:
        asyncio.run(main())
    except KeyboardInterrupt:
        print("Bot turned off")
