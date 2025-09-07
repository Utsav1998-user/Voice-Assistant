📝 **Project Description** 

This is a Python-based Voice Assistant that can listen to user commands, respond with speech, and perform various tasks automatically. It uses speech recognition to convert voice into text and text-to-speech to reply back. The assistant can tell the time, play YouTube videos, search Google or Wikipedia, open websites like Instagram and ChatGPT, and show Windows notifications.

**Libraries and Tools Used**

● **speech_recognition** → Converts your speech into text using Google’s Speech Recognition API.
● **pyttsx3** → Converts text into speech (offline).
● **datetime (built-in)** → To get and speak the current system time.
● **winotify** → Creates Windows 10+ desktop notifications (Assistant started/stopped).
● **webbrowser (built-in)** → Opens websites (YouTube, Google, etc.) in your browser.
● **pywhatkit** → Automates tasks like playing YouTube videos, sending WhatsApp messages, etc.
● **pynput.keyboard** → Listens for keyboard events (e.g., pressing ESC to stop assistant).
● **threading (built-in)** → Allows ESC key listener to run in the background without blocking assistant.
● **sys (built-in)** → General Python system functions (not actively used here but good for exit handling).


🔹 **Libraries Used Before**
● **win10toast** → Earlier,used this for notifications. Works, but has fewer customization options than winotify.
                   works only in pycharm 
● **keyboard** → A simpler keyboard event library, but pynput is more reliable for detecting special keys like ESC.
                 works only in pycharm


🔹 **Why I Built It:**

● To learn Python automation with external libraries
● To understand how speech-to-text and text-to-speech systems work
● To gain hands-on experience in building a mini AI assistant project
● To showcase a practical portfolio project for resumes and interviews

📌 **Notes**

● Requires Python 3.8+
● Works best with a clear microphone input
● Notifications work only on Windows 10/11
● This project is created on python 3.10

💻 **Desktop Application**
📦 **Build EXE (Windows)**

**Liabraries and tools to make desktop application using exe format**
**Liabraries** → Pyinstaller

🔹 1. **Install PyInstaller**
● pip install pyinstaller

🔹 2. **Navigate to Project Folder**

● Open Command Prompt / PowerShell in your project folder (where VoiceAssistant.py is saved).
● cd path\to\your\project

🔹 3. **Build EXE**

● Run PyInstaller with these options:
● pyinstaller --onefile --noconsole --icon=icon.ico VoiceAssistant.py
● --onefile → Packs everything into a single .exe
● --noconsole → Hides the terminal window when running (good for GUI/assistants)
● --icon=icon.ico → (Optional) Adds a custom icon for your assistant

🔹 4. **Find the EXE**

● After the build finishes, check:
● dist/VoiceAssistant.exe
● That’s your standalone application 🎉

🔹 5. **Common Fixes**

● DLL errors: Make sure your Python version matches PyInstaller’s supported versions (e.g., Python 3.10 works best).
● pyaudio missing: Install with

● pip install pipwin
● pipwin install pyaudio

🎤 **Icon**
To use personalize icon on desktop application
use png/jpg images
Icon not showing: Ensure icon.ico is in the same folder as your script.

pyinstaller --onefile --noconsole --hidden-import=pynput.keyboard._win32 --hidden-import=pynput.mouse._win32 Voice_Assistant.py
