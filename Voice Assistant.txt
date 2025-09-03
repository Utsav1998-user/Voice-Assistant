import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import pywhatkit as kit
from pynput import keyboard
from winotify import Notification
import threading
import sys

# Notification function using winotify
def notify(title, message):
    toast = Notification(app_id="Voice Assistant",
                         title=title,
                         msg=message)
    toast.show()

# Global stop flag
stop_flag = False

# ESC key listener
def on_press(key):
    global stop_flag
    try:
        if key == keyboard.Key.esc:
            stop_flag = True
            notify("Voice Assistant", "Stopped by ESC ❌")
            return False  # stop listener
    except:
        pass

def start_esc_listener():
    listener = keyboard.Listener(on_press=on_press)
    listener.start()

# Initialize speech engine and recognizer
engine = pyttsx3.init()
recognizer = sr.Recognizer()

engine.setProperty("rate", 150)   # speed of speech
engine.setProperty("volume", 1.0) # volume (0.0 to 1.0)

def speak(text):
    engine.say(text)
    engine.runAndWait()

def listen():
    with sr.Microphone() as source:
        print("listening...")
        recognizer.adjust_for_ambient_noise(source, duration=0.1)
        print("Listening...")
        audio = recognizer.listen(source)

        try:
            command = recognizer.recognize_google(audio)
            print("You said:", command)
            return command.lower()
        except:
            speak("Sorry, I can't understand.")
            return ""

def run_assistant():
    notify("Voice Assistant", "Assistant started 🚀")
    speak("Hello! I'm your assistant. How can I help you?")
    start_esc_listener()  # Start ESC listener in background

    while True:
        if stop_flag:
            notify("Voice Assistant", "Assistant stopped ❌")
            speak("Goodbye!")
            break

        command = listen()

        if "time" in command:
            now = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {now}")
            print(f"The time is {now}")

        elif "open youtube" in command:
            webbrowser.open("https://www.youtube.com")
            speak("Opening YouTube")

        elif "play" in command:
            query = command.replace("play", "").replace("on youtube", "").strip()
            speak(f"Playing {query} on YouTube")
            kit.playonyt(query)

        elif "open google" in command:
            webbrowser.open("https://www.google.com")
            speak("Opening Google")

        elif "search" in command:
            query = command.replace("type", "").replace("on google", "").strip()
            speak(f"Searching {query} on Google")
            webbrowser.open(f"https://www.google.com/search?q={query}")

        elif "open wikipedia" in command:
            webbrowser.open("https://wikipedia.org")
            speak("Opening Wikipedia")

        elif "search wikipedia" in command:
            query = command.replace("search wikipedia", "").strip()
            speak(f"Searching {query} on Wikipedia")
            webbrowser.open(f"https://en.wikipedia.org/wiki/{query}")

        elif "open instagram" in command:
            webbrowser.open("https://www.instagram.com")
            speak("Opening Instagram")

        elif "open chat gpt" in command or "open gpt" in command:
            webbrowser.open("https://chat.openai.com")
            speak("Opening ChatGPT")

        elif "stop" in command or "quit" in command:
            notify("Voice Assistant", "Assistant stopped ❌")
            speak("Goodbye!")
            break

run_assistant()
