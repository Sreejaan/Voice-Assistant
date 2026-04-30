# Voice Assistant with Twilio and OpenAI (Python)

This project creates a voice assistant that uses [Twilio Voice](https://www.twilio.com/docs/voice) and [ConversationRelay](https://www.twilio.com/docs/voice/twiml/connect/conversationrelay), and the [Open AI API](https://platform.openai.com/docs/api-reference/introduction) that can engage in two-way conversations over a phone call.

## Overview

This application allows users to call a Twilio number and interact with an AI assistant powered by OpenAI's GPT-4o-mini model. The assistant will respond to user queries in natural language.

## Prerequisites

- [Python 3.10+](https://www.python.org/downloads/)
- A Twilio Account: Sign up for a free trial here.
- A Twilio Number with Voice Capabilities: [Instructions to purchase a number.](https://support.twilio.com/hc/en-us/articles/223180928-How-to-Buy-a-Twilio-Phone-Number)
- An Open AI Account and API Key: Visit Open AI's platform [here](https://platform.openai.com/api-keys) for more information.

## Installation

1.  Clone this repository
2.  Install the required dependencies:
   `pip  install  -r  requirements.txt`

4.  Configure your environment variables in the  .env  file:
    - `cp .env.example .env`
    - `OPENAI_API_KEY`: Your OpenAI API key
    - `NGROK_URL`: Your ngrok URL (without https://)

## Usage

1.  Start ngrok to expose your local server:
   `ngrok  http  8080`

3.  Update the  `NGROK_URL`  in your  .env  file with the new URL from ngrok
    
4.  Run the application:
   `python  main.py`

4.  Configure your Twilio phone number to use the  `/twiml`  endpoint as the webhook for incoming calls (https://your-ngrok-url/twiml)
    
5.  Call your Twilio number to interact with the assistant
    

## How It Works

1.  When a user calls the Twilio number, Twilio requests the TwiML from  `/twiml`
2.  The TwiML instructs Twilio to connect to the WebSocket at  `/ws`
3.  Voice input from the user is sent to the server via WebSocket
4.  The server sends the input to OpenAI and gets a response
5.  The response is sent back to Twilio to be converted to speech
6.  The conversation continues until the call ends

## Project Structure

- `main.py`: The main application file containing the FastAPI server, WebSocket handler, and OpenAI integration
- `requirements.txt`: Python dependencies
- `.env`: Environment variables for API keys and configuration
