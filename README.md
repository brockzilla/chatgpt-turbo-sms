
# ChatGPT-Turbo SMS

ChatGPT-Turbo SMS is a Flask application that allows users to send SMS text messages to ChatGPT-Turbo using Twilio and receive instant responses. This application can be run locally or hosted on a services like DigitalOcean to stay active 24/7 using [tmux](https://github.com/tmux/tmux/wiki). The application uses Flask, Twilio, OpenAI, and ngrok.

## Video Demonstration

A video demonstration of the ChatGPT-Turbo SMS application, hosted on DigitalOcean and utilizing tmux to keep the session open after closing the console, is shown below.

https://user-images.githubusercontent.com/63890666/225838063-f71c5a9b-fe22-4882-ab70-b3c20e26ba11.mp4


## Features

-   Send text messages to ChatGPT-Turbo and receive instant responses
-   Utilizes Twilio API for SMS handling and OpenAI API for processing user queries
-   Supports local deployment and also easily deployable on DigitalOcean using tmux for persistent sessions
-   Utilizes ngrok for easy access to the application

## Prerequisites

-   Python 3.6 or later
-   Twilio account with an SMS-enabled phone number
-   OpenAI API key
-   ngrok

## Installation

1.  Clone the repository:
    
    `git clone https://github.com/Kaludii/ChatGPT-Turbo-SMS.git
    cd ChatGPT-Turbo-SMS` 
    
2.  Create and activate a virtual environment:
    
    `python3 -m venv venv
    source venv/bin/activate` 
    
3.  Install the required packages:
    
    `pip install -r requirements.txt` 
    
4.  Copy your Twilio Account SID, Auth Token, and OpenAI API Key to the `.env` file in the project root directory:
    
    `TWILIO_ACCOUNT_SID=your_twilio_account_sid
    TWILIO_AUTH_TOKEN=your_twilio_auth_token
    OPENAI_API_KEY=your_openai_api_key` 
Replace `your_twilio_account_sid`, `your_twilio_auth_token`, and `your_openai_api_key` with the corresponding values from your Twilio and OpenAI accounts.
    

## Usage

### Running the application locally

1.  Start the Flask app:
    
    `python app.py` 
    
2.  In a separate terminal, start ngrok:
    
    `ngrok http 5000` 
    
3.  Configure your Twilio phone number's messaging webhook with the generated ngrok URL followed by `/sms`. For example, if your ngrok URL is `https://abcd1234.ngrok.io`, set the webhook to `https://abcd1234.ngrok.io/sms`.
	
   > Add the webhook URL to the following two Twilio pages, [Phone Numbers > Manage > Active Numbers](https://console.twilio.com/us1/develop/phone-numbers/manage/incoming?frameUrl=/console/phone-numbers/incoming/PN4b2f478c4ce3bdeb706ba139c1468cda?x-target-region=us1), and [Conversations > Manage > Global Webhooks](https://console.twilio.com/us1/develop/conversations/manage/webhooks?frameUrl=/console/conversations/configuration/webhooks?x-target-region=us1). Make sure both are with HTTP POST and for the second link make sure "onMessageAdded" is selected in the Post-webhooks section. Example pictures:

![image](https://user-images.githubusercontent.com/63890666/225839323-dbef5054-87af-48a4-8d0c-516dcc084fd3.png)
    
4.  Send an SMS to your Twilio phone number. ChatGPT-Turbo will process the message and you'll receive an immediate response.
    

### Hosting the application on DigitalOcean

1.  To host the application on DigitalOcean like in the video example shown above, follow these steps:
   > 	a.  Deploy a new Droplet on DigitalOcean.
   >
   > 	b.  Install the required dependencies on the Droplet.
   >
   > 	c.  Clone the repository and configure the `.env` file as described above.
   >
   > 	d.  Start a new `tmux` session:

`tmux new -s chatgpt-turbo-sms` 

2.  Run the application within the `tmux` session:

`python app.py` 

3.  In a separate terminal, start a new `tmux` session:
    
    `tmux new -s chatgpt-turbo-sms-ngrok` 

4.  Start ngrok:

    `start ngrok` 

5.  Run the application within the `tmux` session:

`python app.py` 

6.  Detach from the `tmux` session by pressing `Ctrl-b` followed by `d`.

Your application will continue running even after you close your console. To reattach to the `tmux` session, use:

`tmux attach -t chatgpt-turbo-sms`, and `tmux attach -t chatgpt-turbo-ngrok`

7.  Copy the webhook URL from the ngrok window followed by `/sms`, similar to 3A from the running locally section.

## About the Developer

This app was developed by [Kaludii](https://github.com/Kaludii) using the the different libraries linked above. Kaludii is an AI enthusiast who is passionate about developing and applying large learning models to solve real-world problems quickly and stress-free.
