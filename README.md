# Steps to host your Telegram bot.
### Heroku:

-  Create a Telegram bot with Telegraf API.
-  Create an account on [Heroku](http://heroku.com/).
-  Install [Heroku CLI](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up).
-  Install and [setup Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
-  Add [micro-bot](https://www.npmjs.com/package/micro-bot) to your project:

    ```bash
    npm install micro-bot --save
    ```
- Remove Telegraf dependency from **package.json**.
- Set the start command in **package.json**:
    ```javascript
    ...
"main": "index.js",
"scripts": {
    "start": "micro-bot"
}
    ...
    ```
- Make changes to the code.
    1. Change the telegraf import to:
        ```javascript
        const { Composer } = require('micro-bot');
        ```
    2. Create bot from **Composer:**
        ```javascript
        const bot = new Composer();
        ```
    - Finally remove `bot.launch()` & use this line instead :
        ```javascript
        module.exports = bot
        ```
- Initialize a new git repository:
    ```bash
    git init
    ```
- Make **.gitignore** file with the following content:
    ```
    node_modules
    ```
- Login to Heroku CLI:
    ```bash
    heroku login
    ```
- Create a new Heroku app:
    ```bash
    heroku create
    ```
- Update Heroku config
    ```bash
    heroku config:set --app YourAppId BOT_TOKEN='YOUR BOT TOKEN'
    heroku config:set --app YourAppId BOT_DOMAIN='https://YourAppId.herokuapp.com'
    ```
- Create a **Procfile** file in the root of the bot structure with the following content:
    ```
    web: micro-bot -p $PORT
    ```
- Finally use Git to deploy:
    ```bash
    git add .
    git commit -m 'commit message'
    git push heroku master
    ```

## How to make changes and redeploy the code:
- Just save all changes.
- Run the following commands:
    ```bash
    git add .
    git commit -m 'commit message'
    git push heroku master
    ```