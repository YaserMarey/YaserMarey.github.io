---
title: "Building WhatsApp Chatbot powered by OpenAI GPT-3! - 3" 
layout: home
---
![ Building OpenAI WhatsApp Chatbot](chatgpt_wts_app.png "GPT-3 WhatsApp")
# Building WhatsApp Chatbot powered by OpenAI GPT-3! - 3

### Part - 1: Text Completion using OpenAI Language Models

Follow along as we walk through the steps of building a WhatsApp Chatbot powered by OpenAI GPT-3 using Python, WhatsApp Cloud API, and a FastAPI Webhook published on Heroku.


#### This is part - 2 of a series of three posts, the other two parts are:
#### Part - 1: [Sending Messages using WhatsApp Cloud API](https://yasermarey.github.io/building_openai_whatsapp_1.html)
https://platform.openai.com/docs/api-reference/introduction
#### Part - 2: Receiving Messages from WhatsApp Cloud API using WebHooks


***I will update the links to 3 soon, follow me to receive notifications when it is published***

In part-1 we wrote a simple WhatsApp Cloud API wrapper that sends template and converstaion messages to the cusotmer. In this part we will write a webhook and publish it to Heroku and then configure our Meta chatgpt_wtsapp application to send messages from customers over this webhook to our application.
In part-2, 
In this last part we will use public openai APIs to send and receive text completion to the prompts sent from the customer.

Let's start,

The general steps we need to take for this part are as the following:

1- Write a webhook.

2- Publish the webhook to Heroku

3- Test receving messages from customer test number.


Here are the steps in detail:

***Step 1***
Using your prefered code editor, create webhook.py and copy the code below.

```python
#webhook.py
import os
from fastapi import FastAPI, Request, Response
from fastapi.encoders import jsonable_encoder

from app.whatsapp_client import WhatsAppWrapper
from app.openai_client import OpenAIWrapper

app = FastAPI()

VERIFY_TOKEN = os.environ.get("WHATSAPP_HOOK_TOKEN")

@app.get("/")
def I_am_alive():
    return "I am alive!!"

@app.get("/webhook/")
def subscribe(request: Request):
    if request.query_params.get('hub.verify_token') == VERIFY_TOKEN:
        return int(request.query_params.get('hub.challenge'))
    return "Authentication failed. Invalid Token."

@app.post("/webhook/")
async def process_notifications(request: Request):
    wtsapp_client = WhatsAppWrapper()
    data = await request.json()
    print ("We received " + str(data))
    response = wtsapp_client.process_webhook_notification(data)
    if response["statusCode"] == 200:
        if response["body"] and response["from_no"]:
            openai_client = OpenAIWrapper()
            reply = openai_client.complete(prompt=response["body"])
            print ("\nreply is:"  + reply)
            wtsapp_client.send_text_message(message=reply, phone_number=response["from_no"], )
            print ("\nreply is sent to whatsapp cloud:" + str(response))

    return jsonable_encoder({"status": "success"}, 200)
```
As per Meta documentation, webhook should have two endpoints, GET and POST.
The GET method 

Login to your Facebook developer account and click on the Create App button and choose the ***Business*** type app option and then click the next button below.

![](chatgpt_wts_app_1.png)

We select a name that Meta will use to refer to our application on the application's dashboard, we will choose ***chatgpt_wtsapp***, fill in my email and click next.

![](chatgpt_wts_app_2.png)

The application is created but we need to add a Meta Product to it, in our case this would be ***WhatsApp***. We need to click the Setup button on the WhatsApp product card at the bottom of the page.

![](chatgpt_wts_app_3.png)

One more screen to go, now you just need to select a business account or create one if there is no account created before, and then hit create button.

![](chatgpt_wts_app_4.png)

Now click the "Start Using the API" button and follow on to the next step.

![](chatgpt_wts_app_5.png)

Take note of ***WhatsApp Temporary Access Token***

***Step 2***

Most of the configuration is done now, all that we need to do is to add a phone number to test sending messages to it from WhatsApp Cloud API.

![](chatgpt_wts_app_6.png)

Select that number and now we can test sending the message by hitting "Send Message" or by copying the ```crul``` command to your terminal and running it. Upon doing either of these you should receive a message on the test number you selected, the message should be  similar to this:

![](chatgpt_wts_app_7.png)

Take note of the ***Phone Number ID***.


***Step 3***

Now let's write some code to wrap the WhatsApp Cloud API and use this wrapper in sending a template message similar to the one above and then relay replies we will receive later from OpenAI. 

Fire your preferred code editor, my preference is Visual Studio Code with Python Extensions, and start building a WhatsApp cloud API wrapper:

In the folder you will create your code in, create a virtual environment:
```
python -m venv venv
``` 
Install requests, and python-dotenv

```sh
pip install requests python-dotenv
```
Create ```.env`` file and set the following keys with WhatsApp Temporary Access Token and Phone Number Id from the above steps.
```sh
WHATSAPP_API_TOKEN=
WHATSAPP_CLOUD_NUMBER_ID=
```
Create whatsapp_client.py and copy the following code:
```python
# whatsapp_client.py
import os
import requests
import json
import config
from dotenv import load_dotenv

load_dotenv()

class WhatsAppWrapper:

    API_URL = "https://graph.facebook.com/v15.0/"
    WHATSAPP_API_TOKEN = os.environ.get("WHATSAPP_API_TOKEN")
    WHATSAPP_CLOUD_NUMBER_ID = os.environ.get("WHATSAPP_CLOUD_NUMBER_ID")

    def __init__(self):
        self.headers = {
            "Authorization": f"Bearer {self.WHATSAPP_API_TOKEN}",
            "Content-Type": "application/json",
        }
        self.API_URL = self.API_URL + self.WHATSAPP_CLOUD_NUMBER_ID

    def send_template_message(self, template_name, language_code, phone_number):

        payload = {
            "messaging_product": "whatsapp",
            "to": phone_number,
            "type": "template",
            "template": {
                "name": template_name,
                "language": {
                    "code": language_code
                }
            }
        }

        response = requests.post(f"{self.API_URL}/messages", json=payload,headers=self.headers)

        assert response.status_code == 200, "Error sending message"

        return response.status_code

if __name__ == "__main__":
    client = WhatsAppWrapper()
    # send a template message
    client.send_template_message("hello_world", "en_US", "201012345678")
```

The code is simple, but a couple of things to keep in mind: first it defines one method that sends a ***template whatsapp message*** This type of message is the only one allowed to be sent to customers without them initiating the conversation, so it must be an approved template from Meta.

We will use this method only to test that our code can send messages. In the next section, I am adding another method that we will actually use to send replies from GPT-3. 

The second thing to notice is that in our current development mode, WhatsApp Cloud API only allows sending messages, either template or regular, to up to 5 pre-defined phone numbers. Notice how the phone number is used without leading + or zeros.

To source the virtual environment:
```sh
$ source venv/bin/activate
```
And run the whatsapp client with the following command:

```
$ python whatsapp_client.py
```
If you receive a message successfully then we are done, 
To prepare for the following task of receiving messages and sending replies add the following method to WhatsAppClientWapper class in whatsapp_client.py 

```python
    def send_text_message(self,message, phone_number):
        payload = {
            "messaging_product": 'whatsapp',
            "to": phone_number,
            "type": "text",
            "text": {
                "preview_url": False,
                "body": message
            }
        }
        response = requests.post(f"{self.API_URL}/messages", json=payload,headers=self.headers)
        print(response.status_code)
        print(response.text)
        assert response.status_code == 200, "Error sending message"
        return response.status_code

```
This is the method we will use to send reply messages to the customer once the conversation is initiated. The only difference is the type of message is ```text``` this time and the method will fail if there is no active conversation with the phone number we are sending to.

That's it for Part 1. In Part 2, I'll show you how to receive messages from customers using a webhook and the FastAPI framework. 

Stay tuned!

The complete source code for this series is available [@github](https://github.com/YaserMarey/whatsapp_openai_chatbot)

----
Salam
