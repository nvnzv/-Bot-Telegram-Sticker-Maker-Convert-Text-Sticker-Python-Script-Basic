# BOT TELEGRAM STICKER MAKER BASIC
# Navanza Digital Lab
# Cara pakai:
# 1. Ganti 'YOUR_TELEGRAM_BOT_TOKEN' dengan token botmu
# 2. Jalankan script ini (python bot.py)
# 🔥 Untuk versi premium dengan auto delete command dan multi group support, beli di Lynk: https://lynk.id/nvnzv

import telebot
from PIL import Image, ImageDraw, ImageFont
import os

TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"
bot = telebot.TeleBot(TOKEN)

@bot.message_handler(func=lambda message: True)
def text_to_sticker(message):
    text = message.text
    img = Image.new('RGBA', (512, 512), (255, 255, 255, 0))
    draw = ImageDraw.Draw(img)
    font = ImageFont.load_default()
    draw.text((10, 250), text, font=font, fill=(0,0,0,255))
    img.save('sticker.png')
    
    with open('sticker.png', 'rb') as sticker:
        bot.send_sticker(message.chat.id, sticker)
    
    os.remove('sticker.png')

bot.infinity_polling()
