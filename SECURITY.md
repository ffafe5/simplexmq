Good greetings, my post has nothing to do with security policies. I am reaching out to you about your comment in this locked thread:
https://github.com/pyinstaller/pyinstaller/issues/6462
You probably don't care about this anymore, but I found a way to make it work if you don't mind another 20MB on your exe size:
Store a python virtual environment inside of the outermost EXE that you created first, and have that outer EXE use subprocess to initiate a python session inside of the bundled venv executable.
Your code (running in the outer exe) thus runs a separate python instance where sys.executable has a normal pythonic meaning, and so can call upon another instance of PyInstaller.
I have this running such that the initial generator runs in a python venv, and packages its own venv into its generated exe. That generated exe then uses a copy of that venv to run pyinstaller again.
