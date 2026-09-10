# cafe-delvann-botimport os
from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes

TOKEN = os.getenv("BOT_TOKEN")


async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "🎉 به ربات Cafe Delvann خوش آمدید!\n\n"
        "برای دریافت لینک دعوت اختصاصی خودتان، دستور زیر را بزنید:\n"
        "/invite\n\n"
        "برای مشاهده رتبه دعوت‌ها:\n"
        "/rank"
    )


async def invite(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user = update.effective_user

    await update.message.reply_text(
        f"سلام {user.first_name} 🌹\n\n"
        "🔗 لینک دعوت اختصاصی شما به‌زودی فعال می‌شود.\n\n"
        "با دعوت دوستانتان به جمع Cafe Delvann کمک کنید بزرگ‌تر و شادتر بشیم 🎉"
    )


async def rank(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "🏆 رتبه‌بندی دعوت‌کنندگان\n\n"
        "این بخش پس از اتصال سیستم شمارش دعوت‌ها فعال می‌شود."
    )


def main():
    if not TOKEN:
        raise ValueError("BOT_TOKEN is not set")

    app = Application.builder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("invite", invite))
    app.add_handler(CommandHandler("rank", rank))

    print("Cafe Delvann Bot is running...")
    app.run_polling()


if __name__ == "__main__":
    main()
