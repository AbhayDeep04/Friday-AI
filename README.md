# Friday AI

Friday AI is an interactive speech recognition and response system that uses OpenAI's GPT-3.5-turbo model to generate responses to user queries. This project leverages the `speech_recognition` library to convert spoken words into text, processes the text with GPT-3.5, and then uses the `gtts` library to convert the text response back into speech.
You can change the context of your voice bot by modifying the sentence inside the 'messages' array initialization.

## Features

- **Speech-to-Text:** Converts user speech into text using Google Web Speech API.
- **AI Response Generation:** Uses OpenAI's GPT-3.5-turbo model to generate responses based on the converted text.
- **Text-to-Speech:** Converts the AI-generated text response into speech using Google's Text-to-Speech (gTTS).
- **Context Maintenance:** Maintains conversation context by storing previous messages.

## Prerequisites

- Python 3.6 or higher
- An OpenAI API key
- Required Python libraries: `speech_recognition`, `openai`, `gtts`, `mpg321`

