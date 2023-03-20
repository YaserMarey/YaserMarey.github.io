---
layout: post
title: "Building WhatsApp Chatbot powered by OpenAI GPT-3! - 2" 
categories: [NLP, OpneAI]
excerpt: Follow along as we walk through the steps of building a WhatsApp Chatbot powered by OpenAI GPT-3 using Python, WhatsApp Cloud API, and a FastAPI Webhook published on Heroku.
---

![Building OpenAI WhatsApp Chatbot](chatgpt_wts_app.png "GPT-3 WhatsApp")

## Receiving Messages from WhatsApp Cloud API using Webhooks

In Part 1, we wrote a simple WhatsApp Cloud API wrapper that sends template messages. We also added a method to send conversation messages to the customer, provided that the customer opts into a conversation with us.

In this part, we will write a webhook and publish it to Heroku. Then, we will configure our Meta Cloud API chatgpt_wtsapp application, which we created in Part 1, to relay messages from customers to our application through this webhook.

Let's start! The steps we need to take are as follows:

## Steps
1. Write webhook subscribe and callback methods
2. Publish the webhook to Heroku
3. Configure the webhook on the Meta application dashboard
4. Test receiving messages from a customer test number

Here are the steps in more detail:


***Step 1***

Using your preferred code editor, create webhook.py and copy the code below:

```python
# webhook.py
import os
from fastapi import FastAPI, Request, Response
from fastapi.encoders import jsonable_encoder

from app.whatsapp_client import WhatsAppClient

app = FastAPI()

WHATSAPP_HOOK_TOKEN = os.environ.get("WHATSAPP_HOOK_TOKEN")

@app.get("/")
def I_am_alive():
    return "I am alive!!"

@app.get("/webhook/")
def subscribe(request: Request):
    print("subscribe is being called")
    if request.query_params.get('hub.verify_token') == WHATSAPP_HOOK_TOKEN:
        return int(request.query_params.get('hub.challenge'))
    return "Authentication failed. Invalid Token."

@app.post("/webhook/")
async def callback(request: Request):
    print("callback is being called")
    wtsapp_client = WhatsAppClient()
    data = await request.json()
    print ("We received " + str(data))
    response = wtsapp_client.process_notification(data)
    if response["statusCode"] == 200:
        if response["body"] and response["from_no"]:
            reply = response["body"]
            print ("\nreply is:"  + reply)
            wtsapp_client.send_text_message(message=reply, phone_number=response["from_no"], )
            print ("\nreply is sent to whatsapp cloud:" + str(response))

    return {"status": "success"}, 200
```

And in whatsapp_client.py we created in part-1, we want to add ```process_notification``` as the following:

```python
    # whatsapp_client.py
    def process_notification(self, data):
        entries = data["entry"]
        for entry in entries:
            for change in entry["changes"]:
                value = change["value"]
                if value:
                    if "messages" in value:
                        for message in value["messages"]:
                            if message["type"] == "text":
                                from_no = message["from"]
                                message_body = message["text"]["body"]
                                prompt = message_body
                                print(f"Ack from FastAPI-WtsApp Webhook: {message_body}")
                                return {
                                    "statusCode": 200,
                                    "body": prompt,
                                    "from_no": from_no,
                                    "isBase64Encoded": False
                                }

        return {
            "statusCode": 403,
            "body": json.dumps("Unsupported method"),
            "isBase64Encoded": False
        }

```

As per [Meta documentation](https://developers.facebook.com/docs/graph-api/webhooks/getting-started), webhook should implement two methods to process ***Subscribe*** and ***Callback*** requests.

The ```subscribe``` method handles HTTP GET requests and should receive three query parameters from Meta those are: ```hub.mode```, ```hub.challenge```, and ```hub.verify_token```, such as the following:

```sh
curl -X GET "https://path_to_your_webhook/webhook/?hub.mode=subscribe&hub.challenge=638585501&hub.verify_token=HELLO"
```

In ```subscribe``` method in the code above, upon receiving a GET request from Meta Cloud API, we need to check the token sent from Meta Cloud API and compare it to our application token. I am using an arbitrary string "HELLO" and if it matches then we need send back the received challenge numeric value sent to us with the request.

Meta Cloud API will call this subscribe method at the time of configuration to verify our webhook.

The ```callback``` method handles HTTP POST requests and processes the notification, those are any changes that we configure Meta Cloud API to let us know about, for example, new WhatsApp messages. 

The notification schema is verbose since it can be used to update us on many different types of changes and we will need to navigate the notification structure to find the message. 

The typical request payload sent from Meta to our application should look similar to the following:

```sh
{
'object': 'whatsapp_business_account', 
'entry': [
            {
            'id': '101648795904090', 
            'changes': [
                        {
                            'value': {
                                    'messaging_product': 'whatsapp', 
                                    'metadata': {
                                                'display_phone_number': '15550311009', 
                                                'phone_number_id': '111679144885464'
                                                }, 
                                    'contacts': [
                                                    {
                                                    'profile': {'name': 'Yaser Marey'}, 
                                                    'wa_id': '201012345678'
                                                    }
                                                ], 
                                    'messages': [
                                                    {
                                                    'from': '201012345678', 
                                                    'id': 'wamid.********', 
                                                    'timestamp': '1675555786', 
                                                    'text': 
                                                            {
                                                                'body': 'How are you'
                                                            }, 
                                                    'type': 'text'
                                                    }
                                                ]
                                        }, 
                            'field': 'messages'
                        }]
            }
        ]
}

```
Notice how an entry is an array, and changes are another nested array in each entry, and each change could be a message or something else, for example, a photo upload or a Facebook post, in our case, we are interested only in WhatsApp text messages, therefore, we check if there is the message and message type is text, our response then just echos back the body of the message we received.

To deploy our ***webhook.py*** to Heroku we need three files. ***First*** is ```Procfile``` which is used by Heroku to declare how an app should run. The Procfile specifies the commands that are executed by the app on startup.

Create a text file, add the following line, and save it to the root of our project source folder:
```sh
web: gunicorn -w 4 -k uvicorn.workers.UvicornWorker app.webhook:app
```

***Second*** is ```runtime.txt``` file that specifies the version of Python that will be used to run the app. The file ensures that the correct version of Python is installed on the Heroku dyno.

Create a text file, add the following line, and save it to the root of our project source folder: 
```sh
python-3.10.4
```

***Third*** we also need ```requirements.txt``` file, we can generate this file using pipreqs, first install it using ```pip```
```sh
$ pip install pipreqs
```
then 
```sh
$ pipreqs .
```
And the resulting file should look like this:

```sh
fastapi==0.89.1
python-dotenv==0.21.1
requests==2.22.0
uvicorn==0.20.0
gunicorn==20.1.0
```
Notice, that pipreqs won't pick uvicorn and gunicorn so you probably need to add them yourself.

***Step 2***


Now, head to [heroku.com](https://id.heroku.com/login), and create an account, you will need a credit card for that but don't worry Heroku will give you 550 dyno hours which is approximately 23 days of continuous usage with a single web dyno which is more than enough for our application here. 

Official Meta documentation describes other methods to publish webhook but I found Heroku the most straightforward.

Create a new application on Heroku
![](chatgpt_wts_app_8_.png "Create New Heroku Application")

Choose a name and click create ***Create App***
![](chatgpt_wts_app_9_.png "Create New Heroku Application")

We have now an application created, we can see it on the Heroku dashboard
![](chatgpt_wts_app_9__.png "Create New Heroku Application")

Set environment variables from the application dashboard then ***settings*** tab
![](chatgpt_wts_app_10_.png "Create New Heroku Application")

Add the following environment variables:
![](chatgpt_wts_app_10__.png "Create New Heroku Application")
In Part-3, we will add OPENAI_API_KEY, keep it empty for now.

We deploy to Heroku by pushing the source to a Heroku git repository that Heroku associates with our application.
From the Heroku application dashboard ***deploy*** page, follow the link to install Heroku CLI and then log in:

```sh
$ heroku login
```

Initialize a repo in the root folder of your project source:

```sh
$ git init
```

Add a remote link to Heroku repository

```sh
$ git remote add heroku https://git.heroku.com/whatsapp-openai-chatbot-app.git
```

Stage all source files we created and commit them.

```sh
$ git add .; git commit -am"my first commit"
```

Now we can deploy through git push as the following

```sh
$ git push heroku master
```

You can see Heroku deploying your application from the logs:
![](chatgpt_wts_app_11_.png "Application logs")

If the build is successful then you can start your application from the dashboard
![](chatgpt_wts_app_10___.png "Create New Heroku Application")

or using the command line

```sh
$ heroku open
```

In both cases you should see a new browser tab like this:
![](chatgpt_wts_app_12.png "Create New Heroku Application")


***step 3***

Login to your Meta Developer Account and click on your app, now from the right side menu select ***WhatsApp>Configuration*** then click edit to configure the URL to the Heroku published webhook we created in step 1, and 2. 

Fill in the URL and the arbitrary string that Meta will send with a subscription request and we can check to verify that the request is authentic.

![](chatgpt_wts_app_13.png)

We also need to subscribe to messages. Click on the ***Manage*** button on the ***WhatsApp>Configuration*** page. Click ***Subscribe***

![](chatgpt_wts_app_14.png)


***Step 4***

We now can test your webhook by sending a message to the WhatsApp Meta Cloud API Business number we received a template message on before in part 1 of this series, and if things went ok then we should see it echoed back to us.

![](chatgpt_wts_app_15.png)

If anything went wrong we can check Heroku Logs.

Great!, we are done with this part. In Part 3, We will pass the message we received from the customer over webhook as a prompt to OpenAI GPT-3 and ask it to complete it and then respond with the reply to the customer.

Stay tuned!

The complete [source code](https://github.com/YaserMarey/whatsapp_openai_chatbot) for this series is available [@github](https://github.com/YaserMarey/whatsapp_openai_chatbot)

----
Salam,
