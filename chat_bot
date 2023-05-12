from telegram.ext import Updater, Filters, MessageHandler
import datetime
import locale


locale.setlocale(locale.LC_ALL, 'ru_RU')


updater = Updater(token='TOKEN')

def say_hi(update, context):
    chat = update.effective_chat
    context.bot.send_message(chat_id=chat.id, text='Привет, я бот, который ответит какой день недели!'
                            ' Отправь дату в формате дд/мм/год, чтобы узнать день недели, например: 09.07.1911')

def get_date(update, context):
    try:
        date_str = update.message.text
        date_obj = datetime.datetime.strptime(date_str, '%d.%m.%Y')
        day_of_week = date_obj.strftime('%A')
        chat = update.effective_chat
        context.bot.send_message(chat_id=chat.id, text=day_of_week)
    except ValueError:
        context.bot.send_message(chat_id=update.effective_chat.id, 
                                 text='Неверный формат даты. Пожалуйста, отправьте дату в формате день.месяц.гггг.')


updater.dispatcher.add_handler(MessageHandler(Filters.regex(r'\d{1}.\d{1}.\d{4}'), get_date))

updater.dispatcher.add_handler(MessageHandler(Filters.text, say_hi))


updater.start_polling()
updater.idle()
