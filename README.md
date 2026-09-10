import os
from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes

TOKEN = os.environ["BOT_TOKEN"]


async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "🎉 به Cafe Delvann خوش آمدید!\n\n"
        "برای دریافت لینک دعوت خود، /invite را بزنید.\n"
        "برای مشاهده رتبه دعوت‌ها، /rank را بزنید."
    )


async def invite(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "🔗 لینک دعوت اختصاصی شما به‌زودی فعال می‌شود.\n\n"
        "دوستانتان را به Cafe Delvann دعوت کنید 🎉"
    )


async def rank(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "🏆 رتبه‌بندی دعوت‌کنندگان\n\n"
        "سیستم شمارش دعوت‌ها در مرحله بعد فعال می‌شود."
    )


def main():
    app = Application.builder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("invite", invite))
    app.add_handler(CommandHandler("rank", rank))

    print("Cafe Delvann Bot is running...")
    app.run_polling()


if __name__ == "__main__":
    main()
