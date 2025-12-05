from aiogram import Bot, Dispatcher, types, executor

TOKEN = "8460180687:AAEo2obTsStrqbxweNpKgKVqEw8J1aBTBoQ"
ADMIN_ID = 7800916583

bot = Bot(token=TOKEN)
dp = Dispatcher(bot)

@dp.message_handler(content_types=['text', 'photo', 'video', 'document', 'voice'])
async def forward_all(msg: types.Message):
    if msg.text:
        await bot.send_message(ADMIN_ID, msg.text)
    elif msg.photo:
        await bot.send_photo(ADMIN_ID, msg.photo[-1].file_id)
    elif msg.video:
        await bot.send_video(ADMIN_ID, msg.video.file_id)
    elif msg.document:
        await bot.send_document(ADMIN_ID, msg.document.file_id)
    elif msg.voice:
        await bot.send_voice(ADMIN_ID, msg.voice.file_id)
    
    await msg.answer("✓")

if __name__ == '__main__':
    executor.start_polling(dp, skip_updates=True)
