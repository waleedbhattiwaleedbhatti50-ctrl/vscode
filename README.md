import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser

# Initialize text-to-speech
engine = pyttsx3.init()
engine.setProperty('rate', 170)

def speak(text):
    engine.say(text)
    engine.runAndWait()

def take_command():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.pause_threshold = 1
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        command = recognizer.recognize_google(audio, language='en-in')
        print(f"You said: {command}")
        return command.lower()
    except Exception:
        speak("Sorry, I didn't understand.")
        return ""

def wish_me():
    hour = datetime.datetime.now().hour
    if hour < 12:
        speak("Good morning!")
    elif hour < 18:
        speak("Good afternoon!")
    else:
        speak("Good evening!")
    speak("I am Jarvis. How can I help you?")

# Main Program
if __name__ == "__main__":
    wish_me()
    while True:
        command = take_command()

        if "time" in command:
            time = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {time}")

        elif "open google" in command:
            speak("Opening Google")
(" speak("Opening YouTube")         webbrowser.open("https://www.google.com")

        elif "your name" in command:
            speak("My name is Jarvis")

        elif "exit" in command or "quit" in command:
            speak("Goodbye!")
            break
