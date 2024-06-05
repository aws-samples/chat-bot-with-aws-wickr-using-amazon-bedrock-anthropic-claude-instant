# Chat-bot with AWS Wickr using Amazon Bedrock Anthropic Claude Instant v1

This sample will allow you to deploy a Generative AI chat-bot to your AWS Wickr network. It uses Amazon Bedrock and the Anthropic Claude Instant model for Q&A functionality. 

## Prerequisites and limitations

## Prerequisites

- Access to Amazon Bedrock, and the **anthropic.claude-instant-v1** model enabled 
- An existing AWS Wickr bot username and password
- A supported host with Docker CE installed. This repo was tested on Ubuntu 22.04
- IAM credentials configured on the host in the `~/.aws/config` and `~/.aws/credentials` file (see [here](https://docs.aws.amazon.com/cli/latest/reference/configure/) for details). The user must have the following IAM policy at a minimum (update with your Bedrock region):
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "bedrock:InvokeModel"
            ],
            "Resource": [
                "arn:aws:bedrock:<region>::foundation-model/anthropic.claude-instant-v1"
            ]
        }
    ]
}
```

## Limitations

For privacy reasons, this bot is 'intentionally forgetful', in that it is not aware of your previous questions or answers. This is because we do not wish to store your AWS Wickr conversations within AWS. **NOTE** If the Amazon Bedrock administrator enables [Model invocation logging](https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html) in the Bedrock console, then the queries will be logged and stored as-per their configuration. By default, logging is disabled.

## Installation

1. Clone this repo and then enter the directory.
2. Confirm you are within the repo directory, then zip and compress the contents: `tar czvf software.tar.gz *`. This will leave you with a file called `software.tar.gz`
3. Create the bot folder: `sudo mkdir /opt/WickrIO`
4. Copy this file to /opt/WickrIO: `sudo cp software.tar.gz /opt/WickrIO/`
5. Start the WickrIO container with the following command: `docker run -v /home/ubuntu/.aws:/home/wickriouser/.aws -v /opt/WickrIO:/opt/WickrIO --restart=always --name="bedrock-claude_llm_bot" -ti public.ecr.aws/x3s2s6k3/wickrio/bot-cloud:latest`
6. You will now be at the command line within the bot.

## Configuration

1. Select `yes` if you wish see welcome message on startup
2. Enter `add` when prompted to enter a command
3. Enter the bot username and password when prompted
4. Select `yes` to auto-login
5. When asked to **Enter the bot configuration to use**, enter `import`
6. When asked for the location, enter `/opt/WickrIO`
7. Enter `bedrock-claude-llm_bot` for the integration name

The bot will now install.

8. Enter your Amazon Bedrock region and credential profile when asked
9. When you see **Successfully added record to the database!**, enter `start` and then provide the password when prompted
10. Type `list` to see the status of the bot, it should say **Running** after a few seconds
11. Send a message to the bot!

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
