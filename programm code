import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
import os
import sys
import time
import re
import warnings
warnings.filterwarnings("ignore")
engine = pyttsx3.init()
engine.setProperty('rate', 170)
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id) 
def talk(text):
    print("🎙️ HULK:", text)
    engine.say(text)
    engine.runAndWait()
def take_command():
    listener = sr.Recognizer()
    with sr.Microphone() as source:
        print("🎧 Listening...")
        listener.adjust_for_ambient_noise(source)
        voice = listener.listen(source)
    try:
        command = listener.recognize_google(voice)
        command = command.lower()
        print("🗣️ You said:", command)
    except sr.UnknownValueError:
        talk("Sorry bro, I didn’t catch that.")
        return ""
    except sr.RequestError:
        talk("Network issue with Google service.")
        return ""
    return command
def run_hulk():
    command = take_command()
    if "play" in command:
        song = command.replace("play", "").strip()
        talk(f"Playing {song} on YouTube 🎶")
        pywhatkit.playonyt(song)
    elif "what's the time" in command:
        time_now = datetime.datetime.now().strftime('%I:%M %p')
        talk(f"It’s {time_now} ⏰")
    elif "who is deepika reddy" in command or "who is deepika" in command:
        info = (
            "Deepika Reddy is a passionate B.Tech student specializing in Cyber Security. "
            "She loves coding, builds Python projects, and enjoys sharing knowledge with others 💻"
        )
        talk(info)
    elif "who is" in command:
        person = command.replace("who is", " ").strip()
        try:
            info = wikipedia.summary(person, sentences=1)
            talk(info)
        except:
            talk("Sorry, I couldn’t find information about that person.")
    elif "joke" in command:
        talk(pyjokes.get_joke())
    elif "open chrome" in command:
        chrome_path = "C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe"
        if os.path.exists(chrome_path):
            talk("Opening Chrome 🚀")
            os.startfile(chrome_path)
        else:
            talk("Chrome path not found 😬")
    elif "open code" in command or "open vs code" in command:
        talk("Opening VS Code 💻")
        os.system("code")
    elif "search" in command:
        search_query = command.replace("search", "").strip()
        talk(f"Searching for {search_query} on Google 🌐")
        pywhatkit.search(search_query)
    elif "set a timer for" in command or "set timer for" in command:
        pattern = r"set (a )?timer for (\d+)\s*(second|seconds|minute|minutes)"
        match = re.search(pattern, command)
        if match:
            value = int(match.group(2))
            unit = match.group(3)
            if "minute" in unit:
                seconds = value * 60
            else:
                seconds = value
            talk(f"Timer set for {value} {unit} ⏳")
            print(f"⏳ Waiting for {seconds} seconds...")
            time.sleep(seconds)
            talk("⏰ Time's up!")
        else:
            talk("Please say like 'set a timer for 10 seconds'.")
    elif "exit" in command or "stop" in command:
        talk("Okay bye, see you later 👋")
        sys.exit()
    elif command != "":
        talk("I heard you, but I don’t understand that yet 😅")
print("✅ Script started")  # Debug line
talk("Heyyy! I'm Hulk – your personal voice assistant.")
while True:
    run_hulk()

