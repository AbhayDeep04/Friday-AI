Friday AI
Friday AI is an interactive speech recognition and response system that uses OpenAI's GPT-3.5-turbo model to generate responses to user queries. This project leverages the speech_recognition library to convert spoken words into text, processes the text with GPT-3.5, and then uses the gtts library to convert the text response back into speech.

Features
Speech-to-Text: Converts user speech into text using Google Web Speech API.
AI Response Generation: Uses OpenAI's GPT-3.5-turbo model to generate responses based on the converted text.
Text-to-Speech: Converts the AI-generated text response into speech using Google's Text-to-Speech (gTTS).
Context Maintenance: Maintains conversation context by storing previous messages.
Prerequisites
Python 3.6 or higher
An OpenAI API key
Required Python libraries: speech_recognition, openai, gtts, mpg321
Installation
Clone the repository:

bash
Copy code
git clone https://github.com/AbhayDeep04/Friday-AI.git
cd Friday-AI
Install the required Python libraries:

bash
Copy code
pip install speechrecognition openai gtts
Install mpg321 for playing audio:

bash
Copy code
sudo apt-get install mpg321  # For Debian/Ubuntu-based systems
brew install mpg321          # For macOS
Set your OpenAI API key:
Replace the placeholder in the script with your actual OpenAI API key:

python
Copy code
OPENAI_KEY = "your_openai_api_key_here"
Usage
Run the script:

bash
Copy code
python script_name.py
Interact with Friday AI:

Speak into the microphone when prompted.
Friday AI will listen, process your input, and respond with a generated answer.
To exit, say "exit", "stop", or "terminate".
Code Explanation
Import Libraries
python
Copy code
import speech_recognition as sr
import os
from openai import OpenAI

OPENAI_KEY = "your_openai_api_key_here"
client = OpenAI(api_key=OPENAI_KEY)
Convert Text to Speech
python
Copy code
def SpeakText(command):
    from gtts import gTTS
    lang = 'en'
    tts = gTTS(text=command, lang=lang)
    tts.save("temp.mp3")
    os.system("mpg321 temp.mp3")
    os.remove("temp.mp3")
Record Speech and Convert to Text
python
Copy code
r = sr.Recognizer()

def recordText():
    while True:
        try:
            with sr.Microphone() as source2:
                r.adjust_for_ambient_noise(source2, duration=0.2)
                print("I'm listening")
                audio2 = r.listen(source2)
                MyText = r.recognize_google(audio2)
                return MyText
        except sr.RequestError as e:
            print(f"Could not request result; {e}")
        except sr.UnknownValueError:
            print("Unknown error occurred")
Send Text to GPT-3.5 and Get Response
python
Copy code
def sendToGPT(messages, model="gpt-3.5-turbo"):
    response = client.chat.completions.create(model=model,
                                              messages=messages,
                                              max_tokens=200,
                                              n=1,
                                              stop=None,
                                              temperature=0.5)
    message = response.choices[0].message.content
    messages.append(response.choices[0].message)
    return message
Main Loop
python
Copy code
messages = [{"role": "user", "content": "Act as Armin in the anime series Attack on Titan."}]

while True:
    text = recordText()
    messages.append({"role": "user", "content": text})
    response = sendToGPT(messages)
    SpeakText(response)
    print(response)
    if text.lower() in ["exit", "stop", "terminate"]:
        print("Exiting...")
        break
Contributing
Feel free to contribute to this project by submitting pull requests or reporting issues.

License
This project is licensed under the MIT License.

Acknowledgments
SpeechRecognition
OpenAI
gTTS
Enjoy interacting with Friday AI! If you have any questions or feedback, please feel free to reach out.

