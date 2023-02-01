# BUAT BOT TELEGRAM OPENAI KEK CETJIPITI

1. Buat akun openai terus create api disini : https://platform.openai.com/account/api-keys

2. Buat bot telegram disini : https://t.me/BotFather ikuti intruksinya dan simpen api keys nya.. 

3. Buat folder di desktop kalian namain bebas, open visualcode studio nya..

4. Pastiin sudah terinstall python terbaru sama pip didalemnya juga ygy.. 

5. Buat 2 file baru namain : requirements.txt . terus isi ini 
```
python-telegram-bot==20.0
openai==0.26.4
```
satu lagi namain bot.py dan isi script berikut :
```
import openai
import logging
from telegram import Update
from telegram.ext import filters, Application, CommandHandler, MessageHandler, CallbackContext

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
logger = logging.getLogger(__name__)

openai.api_key = "API_OPENAI"

TOKEN = "API_BOT_TELE"

async def start(update: Update, context: CallbackContext):
    await context.bot.send_message(chat_id=update.effective_chat.id, text="Hi! Saya adalah bot AI. Bagaimana saya bisa membantu Anda hari ini?")

async def respond(update: Update, context: CallbackContext):
    text = update.message.text
    response = openai.Completion.create(
        engine="text-davinci-003",
        prompt= "user: " + text,
        max_tokens=1024,
        n=1,
        stop=None,
        temperature=0.5,
    ).get("choices")[0].text
    await context.bot.send_message(chat_id=update.effective_chat.id, text=response)

def main():
    application = Application.builder().token(TOKEN).build()

    application.add_handler(CommandHandler('start', start))
    application.add_handler(MessageHandler(filters.ALL, respond))

    application.run_polling()

if __name__ == '__main__':
    main()
    
```
jangan lupa ganti dulu API_OPENAI dan API_BOT_TELE nya.. 
6. Copas copas aja nih ya
```
python -m venv env
```
```
env\Scripts\activate
```
```
pip install python-telegram-bot
```
```
pip install openai
```
```
pip install -r requirements.txt
```
# Jalankan 
```
python bot.py
```

# Silahkan explore sendiri dan gunakan sebaik-baiknya ygy..


...
    
