# AI Voice Assistant using Twilio and OpenAI (Python)

This project demonstrates how to build a conversational voice assistant by integrating **Twilio Voice**, **ConversationRelay**, and the **OpenAI API**. The system enables real-time, two-way voice interactions over a phone call.

---

## ## Overview

With this application, users can dial a Twilio phone number and communicate with an AI-powered assistant driven by OpenAI’s **GPT-4o-mini** model. The assistant processes spoken input and replies naturally, creating a seamless conversational experience.

## ## Requirements

Before getting started, ensure you have the following:

*   **Python version:** 3.10 or higher  
*   **Twilio account:** (You can register for a free trial)  
*   **Twilio phone number:** With voice functionality enabled  
*   **OpenAI account:** Along with a valid API key  

---

## ## Setup Instructions

1.  **Clone the project repository** to your local machine.  
2.  **Install all necessary dependencies** using:
    ```bash
    pip install -r requirements.txt
    ```
3.  **Set up environment variables** by creating a `.env` file:
    ```bash
    cp .env.example .env
    ```
4.  **Update the following values** in your `.env` file:
    *   `OPENAI_API_KEY`: Your OpenAI API key
    *   `NGROK_URL`: Your ngrok URL (exclude `https://`)

---

## ## Running the Application

1.  **Launch ngrok** to expose your local server:
    ```bash
    ngrok http 8080
    ```
2.  **Copy the generated URL** and update the `NGROK_URL` value in your `.env` file.
3.  **Start the application**:
    ```bash
    python main.py
    ```
4.  **In your Twilio console**, configure your phone number’s webhook to point to:  
    `https://your-ngrok-url/twiml`
5.  **Call your Twilio number** and begin interacting with the assistant.

---

## ## Workflow Explanation

1.  **Incoming Call:** When a call is made to the Twilio number, Twilio requests instructions from the `/twiml` endpoint.
2.  **Connection:** The response directs Twilio to establish a WebSocket connection at `/ws`.
3.  **Streaming:** The caller’s voice input is streamed to the server via this WebSocket.
4.  **Processing:** The server forwards the input to OpenAI for processing.
5.  **Generation:** OpenAI generates a response, which is sent back to Twilio.
6.  **Speech Synthesis:** Twilio converts the response into speech and plays it to the user.
7.  **Loop:** This loop continues until the call is terminated.

---

## ## File Structure

*   `main.py`: Contains the FastAPI application, WebSocket logic, and OpenAI integration.
*   `requirements.txt`: Lists all Python dependencies required for the project.
*   `.env`: Stores configuration values such as API keys and URLs.
```