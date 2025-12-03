
# co-Author: Below, under security assessment, is what I have changed and done to the code as I got from below the original author.
As our instructions for an easy copy paste into or save as your own script and to be modified for future editions that way you know you've got clean script.
Security Assessment
I have reviewed the script code you provided line-by-line.
 * Verdict: Clean / Safe.
 * Analysis:
   * No Obfuscation: The code is readable plain text. There are no encoded strings (Base64) or eval statements trying to hide commands.
   * Network Activity: The only network activity involves downloading the pve-remove-nag.sh script logic (which is written locally in the script) and standard apt repository URLs (Debian.org and Proxmox.com).
   * System Changes: The script performs standard administrative tasks: modifying APT source lists, disabling specific systemd services (HA/Corosync), and patching a Javascript file to remove the UI subscription banner.
   * Malice: There is no code intended to exfiltrate data, open reverse shells, or grant unauthorized access.
Modifications Made
Per your request, I have edited the script to:
 * Remove ASCII Art: The header_info function now only clears the screen and prints a simple text line.
 * Enforce Versioning: Modified the logic to strictly reject any version lower than Proxmox VE 9.1.
 * Cleanup: Removed the code blocks related to Proxmox VE 8 (Bookworm) entirely to streamline the file.
Modified Script
Save this file as post-install.sh.
#!/usr/bin/env bash
# Copyright (c) 2021-2025 tteck
# Author: tteckster | MickLesk (CanbiZ)
# License: MIT
# https://github.com/community-scripts/ProxmoxVE/raw/main/LICENSE



Here is the step-by-step guide to transferring the script to your Proxmox server and running it.
There are two main ways to do this. Option 1 is usually the fastest.
Option 1: The "Copy & Paste" Method (Recommended)
This method involves creating a blank file on the server and pasting the code directly into it.

1. Connect to your Proxmox Server

It is highly recommended to use a standard terminal on your computer (Command Prompt, PowerShell, or Terminal) rather than the "Console" inside the web browser, as pasting large blocks of text into the browser console often fails or creates formatting errors.
 
 * Open your computer's terminal.
 * Type: ssh root@<YOUR-PROXMOX-IP>
 * Enter your password.
2. Create the file

We will use nano, a simple text editor built into Linux.
Run:

nano post-install.sh

3. Paste the code
 * Copy the code block I provided in the previous message.
 * Go back to your terminal window.
 * Paste it:
   * Windows (PuTTY/PowerShell): Usually Right-Click the mouse window.
   * Mac/Linux: Cmd+V or Ctrl+Shift+V.
4. Save and Exit
 * Press Ctrl + O (Letter O) to write the file.
 * Press Enter to confirm the name.
 * Press Ctrl + X to exit the editor.
5. Make it Executable
You need to tell Linux this file is a program, not just text.
chmod +x post-install.sh

6. Run the Script
./post-install.sh

Option 2: Uploading via SFTP (If Copy/Paste fails)
If you aren't comfortable with the terminal editor, you can save the file on your computer and upload it.
 * Save the file locally:
   * Copy the code I gave you.
   * Open Notepad (Windows) or TextEdit (Mac).
   * Paste the code.
   * Important: Save the file as post-install.sh. (Make sure it doesn't save as post-install.sh.txt).
 * Upload the file:
   * Use a program like WinSCP (Windows) or Cyberduck (Mac).
   * Connect to your Proxmox IP with username root and your password.
   * Drag the post-install.sh file from your computer to the /root/ folder on the server.
 * Run the script:
   * Go back to your Proxmox Shell.
   * Run these two commands:
     chmod +x post-install.sh
./post-install.sh

Summary Checklist
 * [ ] Version Check: Ensure you are on Proxmox 9.1 or higher (the script will auto-exit if you aren't, but it saves time to check first).
 * [ ] Reboot: The script usually recommends a reboot after it modifies the kernel modules or update sources.
Would you like me to explain what the specific "Debian Trixie" sources in the script actually do, or are you ready to proceed with setting up your first VM?
