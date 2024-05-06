# <div align="center"> ChatGPT Telegram Bot

## How to Install

### Step 1: Install Python

1. Go to the [PyCharm download page](https://www.jetbrains.com/ko-kr/pycharm/download/?section=mac).
3. Click on the appropriate installer for your operating system.
3. Follow the prompts to complete the installation.

### Step 2: Create a Shell script environment

1. Open a terminal or command prompt.
2. Move to the folder containing the script `cd /path/to/directory`
3. Grant script execution permissions `chmod +x init_setup.sh`
4. Run the script with the following command:`./init_setup.sh`


### Step 3: Set up your Telegram bot

1. Create `.env` file and in the `.env` file:
> FLASK_APP=app 
> 
> FLASK_ENV=development
> 
> OPENAI_ORGANIZATION="Your_OPENAI_ORGANIZATION"
> 
> OPENAI_API_KEY="Your_OPENAI_API_KEY"
> 
> TOKEN="Your_TOKEN"
2. See [these instructions](https://core.telegram.org/bots/tutorial#obtain-your-bot-token) for more information on how to do this.
> https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getMe  
or
> https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates
3. `pip install -r requirements.txt`
 
### Step 4: Run the ChatGPT Telegram bot server
1. Open a terminal or command prompt.
2. Navigate to the directory where you installed the ChatGPT Telegram bot.
3. Run `python TeleGPT_bot.py` to start the server.

### Step 6: Chat with your bot in Telegram

1. Open the Telegram app on your device.
2. Find your bot in the list of contacts (you should have already created it with @botfather).
3. `/Start` chatting with your bot.

## Main Code
```python
async def chatgpt(message: types.Message):
    try:
        print(f">>> USER: \n\t{message.text}")
        response = openai.ChatCompletion.create(
            model=MODEL_NAME,
            messages=[
                {"role": "assistant", "content": reference.response},
                {"role": "user", "content": message.text}
            ]
        )
        reference.response = response['choices'][0]['message']['content']
        print(f">>> chatGPT: {reference.response}")
        await bot.send_message(chat_id=message.chat.id, text=f"{reference.response}")
    except openai.error.OpenAIError as e:
        # Log the error and notify the user
        logging.error(f"OpenAI API error: {e}")
        await message.reply("Sorry, I'm currently unable to respond due to API limitations. Please try again later.")
```


