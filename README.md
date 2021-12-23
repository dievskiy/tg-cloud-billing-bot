Telegram bot logic that sends daily notifications about current costs of the AWS infrastructure.

![](https://i.imgur.com/V8ygygi.jpg)

The setup is being deployed into AWS using CloudFormation. Deployed resources are:
* EventBridge rule
* SNS topic
* Lambda function that fetches current costs from AWS and publishes a message to the SNS
* Lambda function subscribed to SNS that parses the message and sends it to the telegram chat
* IAM rules for both lambdas

## how to use
Follow these steps to deploy the setup:
1. Create a bot in telegram using BotFather
2. Create a chat in telegram and add the bot as an admin
3. ```aws cloudformation create-stack --stack-name tg-billing  --template-body file://template.yaml --parameters ParameterKey=BotToken,ParameterValue='xxx:yyy' ParameterKey=TgChatId,ParameterValue='-10xxx' ```
   
Where *BotToken* is a token you received from BotFather and TgChatId is [id of the chat](https://stackoverflow.com/questions/32423837/telegram-bot-how-to-get-a-group-chat-id). You can also change time when billing lambda is triggered by overriding *CronExpression* parameter. By default, it is 18 PM UTC. 

