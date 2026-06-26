Markdown
# Challenge: SUDO MAKE ME A SANDWICH

## 📊 Challenge Info
* **Platform:** picoCTF (via CyLab Security Academy)
* **Category:** General Skills
* **Difficulty:** Easy
* **Points:** 50

## 📝 Description
Can you read the flag? I think you can!

**Connection Command:**
```bash
ssh -p 54899 ctf-player@green-hill.picoctf.net
# Password: 8b23dc85
💡 Hints
What is sudo?

How do you know what permission you have?

🛠️ Solution Walkthrough
1. Connecting to the Machine
Connect to the challenge server using the provided SSH credentials:

Bash
ssh -p 54899 ctf-player@green-hill.picoctf.net
When prompted, enter the password: 8b23dc85

2. Identifying the Roadblock
Running a direct sudo cat flag.txt fails because the server explicitly blocks the user from executing /usr/bin/cat as root.

To find out what we are allowed to do, we check our current user's administrative privileges:

Bash
sudo -l
The output reveals that ctf-player has passwordless sudo rights to run the text editor: /bin/emacs.

3. Exploiting Emacs (GTFOBins Shell Escape)
Because Emacs is running with root privileges, we can use its built-in features to spawn an interactive shell that inherits those same root privileges.

Launch Emacs with sudo:

Bash
sudo /bin/emacs
Once inside the editor, open the command prompt by pressing Alt + X (or Esc then X).

Type shell and hit Enter.

This drops us into an interactive root terminal session. We can confirm our identity and read the flag unhindered:

Bash
whoami # Returns 'root'
cat flag.txt

flag
picoCTF{ju57_5ud0_17_9a782247}
