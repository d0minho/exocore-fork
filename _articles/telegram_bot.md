---
published: true
topic:
subtitle:
date: 2023-10-26
tags: 
---

#  The Redacted Telegram bot 

hello friends. I wanted to add a spam bot to a telegram but every bot i found was way complex for no reason. because of this i decided to code my own bot with ai of course. So to make your life easier I wanted to provide a simple copy paste no code guide to setting up your own telegram spam bot. So lets begin 

## Setting Up a Telegram Bot from Scratch

### 1. **Installing VS Code**:

Visual Studio Code is a free and open-source editor that provides great support for Python and many other languages.

#### For Windows, MacOS, and Linux:

1. Visit the official download page: [Visual Studio Code](https://code.visualstudio.com/download)
2. Download the version suitable for your OS (Windows, MacOS, Linux).
3. Follow the installation instructions specific to your OS.

#### Extensions:

After installation, consider adding the Python extension for enhanced Python support:

1. Open VS Code.
2. Go to Extensions (you can use the shortcut `Ctrl+Shift+X`).
3. Search for `Python` and install the one published by Microsoft.

---



### 1. **Installing Python**:

#### For Windows:

1. Download Python from the official website:
   [Python for Windows](https://www.python.org/downloads/windows/)
2. Launch the installer.
3. Ensure the checkbox "Add Python X.X to PATH" is selected for easy command line access.
4. Click on "Install Now".

#### For MacOS:

1. Use Homebrew: 
   ````
   bash
   brew install python

### **installing the telegram bot** 
open VS CODE. create a python file. save is what you want to name it. open the terminal in VS CODE and type this 

````pip install python-telegram-bot==12.8.0 

### **Set up your bot with bot father**

. Set up Your Bot with BotFather:

If you haven’t created a bot already, talk to the **BotFather** on Telegram to create one.
The BotFather will provide a **TOKEN**. Replace the placeholder TOKEN in your code with this token.
 Getting the CHAT_ID:
This seems to be a group chat ID since it starts with -100.

the easiest way to get a chat id is to add a bot called @getchatid to the group and it will give you this info mation. 

### ** configure your bot**

###### here is the code for the bot

``````
from telegram import Bot, Update
from telegram.ext import CommandHandler
import logging
import threading
import time

# Enable logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
                     level=logging.INFO)
logger = logging.getLogger(__name__)

TOKEN = "ADD THE TOKEN OF YOUR BOT HERE :3"
CHAT_ID = "ADD THE TOKEN OF YOUR CHAT ID HERE :3"

def send_periodic_message(bot):
    while True:
        bot.send_message(chat_id=CHAT_ID, text="THIS IS YOUR CUSTOM MESSAGE :3")
        time.sleep(300)

def start(bot, update):
    chat_id = update.message.chat_id
    bot.send_message(chat_id=chat_id, text="Bot has started!")

def main():
    bot = Bot(TOKEN)
    update_id = None

    # Command handlers
    start_handler = CommandHandler("start", start)
    
    # Start the thread for sending periodic messages
    t = threading.Thread(target=send_periodic_message, args=(bot,))
    t.start()
    
    while True:
        for update in bot.get_updates(offset=update_id, timeout=10):
            if update.message:
                if update.message.text == "/start":
                    start(bot, update)
                update_id = update.update_id + 1

        time.sleep(1)

if __name__ == '__main__':
    main()
`````` 

anyplace you see a :3 replace whats in the quotes with your custom info

## **Run the Bot:**
Navigate to the directory containing your script and run:

````
 python your_script_name.py 
