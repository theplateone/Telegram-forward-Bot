import logging
from telegram import Bot, Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

# 設定 Telegram Bot 的 API Token
TOKEN = '你的Telegram Bot的API Token'

# 設定 A 頻道的 ID
A_CHANNEL_ID = -1001234567890  # 替換為 A 頻道的 ID

# 設定 B 頻道的 ID
B_CHANNEL_ID = -1009876543210  # 替換為 B 頻道的 ID

# 設定日誌紀錄等級
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

def forward_message(update: Update, context):
    message = update.effective_message
    chat_id = message.chat_id

    # 只處理 A 頻道的訊息
    if chat_id == A_CHANNEL_ID:
        # 將訊息轉發到 B 頻道
        context.bot.forward_message(chat_id=B_CHANNEL_ID, from_chat_id=chat_id, message_id=message.message_id)

def main():
    # 建立 Bot 物件
    bot = Bot(token=TOKEN)

    # 建立 Updater 物件
    updater = Updater(bot=bot)

    # 建立指令處理器
    dp = updater.dispatcher

    # 設定訊息處理器
    dp.add_handler(MessageHandler(Filters.chat(chat_id=A_CHANNEL_ID), forward_message))

    # 開始接收和處理更新
    updater.start_polling()

    # 持續運行直到程式被中斷
    updater.idle()

if __name__ == '__main__':
    main()
