# Ska-arena-botimport 
logging import os
from aiogram import Bot, Dispatcher, types
from aiogram.utils import executor

API_TOKEN = os.getenv("API_TOKEN")  # Render возьмёт токен из переменных окружения

logging.basicConfig(level=logging.INFO)
bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)

@dp.message_handler(commands=["start"])
async def start_cmd(message: types.Message):
    keyboard = types.ReplyKeyboardMarkup(resize_keyboard=True)
    buttons = ["Схема арены", "Оплатить парковку", "Афиша", "VIP Ложи", "Связаться с ареной"]
    keyboard.add(*buttons)
    await message.answer("Добро пожаловать в бот СКА Арены!", reply_markup=keyboard)

@dp.message_handler(lambda message: message.text == "Схема арены")
async def arena_scheme(message: types.Message):
    await message.answer("Схема арены: https://ska-arena.ru/scheme")

@dp.message_handler(lambda message: message.text == "Оплатить парковку")
async def pay_parking(message: types.Message):
    await message.answer("Оплата парковки: https://example.com/pay_parking")

@dp.message_handler(lambda message: message.text == "Афиша")
async def poster(message: types.Message):
    await message.answer("Афиша мероприятий: https://ska-arena.ru/poster")

@dp.message_handler(lambda message: message.text == "VIP Ложи")
async def vip_info(message: types.Message):
    await message.answer("VIP ложи: https://ska-arena.ru/vip\nХотите оставить заявку? Напишите нам!")

@dp.message_handler(lambda message: message.text == "Связаться с ареной")
async def contact(message: types.Message):
    await message.answer("Контакты:\nТел: +7 (812) 123-45-67\nEmail: info@ska-arena.ru")

if name == "__main__":
    executor.start_polling(dp, skip_updates=True)
