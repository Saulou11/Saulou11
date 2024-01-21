from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

def start(update, context):
    update.message.reply_text('Olá! Eu sou o seu bot de sinais para a roleta. Envie /sinais para receber os sinais.')

def tiers_du_cylindre(update, context):
    numeros_tiers = [27, 13, 36, 11, 30, 8, 23, 10, 5, 24, 16, 33]
    update.message.reply_text(f'Sinais Tiers du Cylindre: {numeros_tiers}')

def orphelins(update, context):
    numeros_orphelins = [1, 6, 9, 14, 17, 20, 31, 34]
    update.message.reply_text(f'Sinais Orphelins: {numeros_orphelins}')

def voisins_du_zero(update, context):
    numeros_voisins_zero = [22, 18, 29, 7, 28, 12, 35, 3, 26, 0, 32, 15, 19, 4, 21, 2]
    update.message.reply_text(f'Sinais Voisins du Zéro: {numeros_voisins_zero}')

def handle_message(update, context):
    message_text = update.message.text.lower()
    if '/sinais' in message_text:
        update.message.reply_text('Escolha uma estratégia:\n/sinais_tiers\n/sinais_orphelins\n/sinais_voisins_zero')
    else:
        update.message.reply_text('Desculpe, não entendi. Envie /sinais para receber os sinais.')

def main():
    updater = Updater(token='6542728432:AAElfC_Gy5FqI3HM7B358ix0XCPPT8BfxC4', use_context=True)
    dp = updater.dispatcher

    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("sinais_tiers", tiers_du_cylindre))
    dp.add_handler(CommandHandler("sinais_orphelins", orphelins))
    dp.add_handler(CommandHandler("sinais_voisins_zero", voisins_du_zero))
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, handle_message))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
