import telebot

token = "6541284087:AAEjz_G4juS2F718GpnxQsyQx-ezLh1ynJY"
bot =telebot.TeleBot(token)
HELP = """
/help - напечатать справку по программею
/buy1 - заказать клубнику (после /buy пишем дату(без пробелов) ,пробел, пишем виды клубники (/assortment) ,пробел, название аккаунта(чтоб найти нужно название аккаунта : нужно выйти из чата, нажать на три линии сверху слева, затем настройки, зайти в "мой аккаунт" имя пользователя ),вес (в кг))
/buy2 - заказать что то другое (после /buy2 пишем дату ,пробел, то что мы хотим заказать (/assortment) ,пробел,  пробел, название аккаунта(чтоб найти нужно название аккаунта : нужно выйти из чата, нажать на три линии сверху слева, затем настройки, зайти в "мой аккаунт" имя пользователя ), вес(в кг))
https://mykaleidoscope.ru/uploads/posts/2021-10/1634751303_100-mykaleidoscope-ru-p-klubnika-124.jpg
по вопросам - @Belaev_nikita
"""
ASSORTMENT = """ Клубника:
клубника Мальва = 2000 за кг
клубника Сан-Андресс = 3000 за кг
Остальное:
огурцы = 1500 за кг
помидоры = 1500 за кг

"""
@bot.message_handler(commands=["buy1"])
def buy1 (message):
    command = message.text.split(maxsplit = 4)
    date = command[1].lower()
    task = command[2]
    name = command[3]
    number = command[4]
    add_todo(date, task)
    text = " заказали " + task + " " + number + "кг" + "  на дату "+ date + " на имя " + name
    print(message.text,)
    bot.send_message(message.chat.id, "Команда сработала ")
    bot.send_message(message.chat.id, "Вы " + text)
    bot.send_message(1845226135, text)
todos = dict()
tasks = {}
def add_todo(date, task):
    date = date.lower()
    if todos.get(date) is not None:
        todos[date].append(task)
    else:
        todos[date] = [task]
@bot.message_handler(commands=["buy2"])
def buy2 (message):
    command = message.text.split(maxsplit = 4)
    date = command[1].lower()
    task = command[2]
    name = command[3]
    number = command[4]
    add_todo(date, task)
    text = "заказали " + task + " " + number + "кг" + "  на дату "+ date + " На имя " + name
    print(message.text)
    bot.send_message(message.chat.id, "Команда сработала ")
    bot.send_message(message.chat.id,"Вы " + text)
    bot.send_message(1845226135, text)
@bot.message_handler(commands=["help"])
def help(message):
    bot.send_message(message.chat.id, HELP)
@bot.message_handler(commands=[ "assortment"])
def assortment(message):
    bot.send_message(message.chat.id, ASSORTMENT)
@bot.message_handler(commands=[ "start"])
def start(message):
    bot.send_message(message.chat.id, "здраствуйте" + HELP)
bot.polling(none_stop=True)
