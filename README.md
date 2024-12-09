# Network-Traffic-Analysis-with-TCPDump
In this project, the goal was to utilize TCPDump to capture and analyze TCP traffic. This project uses Linux commands, pipes, and input/output redirection.
## Objectives

-Utilize TCPDump to monitor and capture TCP network traffic<br>
-Develop Linux scripts for cyber forensics<br>
-Analyze and decrypt the contents of captured network traffic<br>

### Skills Learned

   -Packet Capture and Analysis: Use TCPDump to capture and analyze TCP/IP packets, including filtering traffic for specific details like source, destination, or protocol types<br>
   -Scripting and Automation: Develop Linux shell scripts to automate network monitoring tasks, enhancing operational efficiency<br>
   -Traffic Logging: Build and manage logging tools to record network activities systematically<br>
   -Advanced Filtering Techniques: Apply complex expressions to filter packets effectively, ensuring precise data extraction<br>
   -Dump File Management: Create and handle sequential dump files with specific size and time constraints<br>
   -Network Forensics: Gain insights into analyzing captured traffic for forensic purposes, including extracting valuable information from encrypted or raw data<br>
 
### Tools Used

- TCPDump: A command-line packet analyzer tool used to capture and inspect network traffic.
- Linux Shell: For creating and running scripts to automate tasks and manage network data efficiently.
- Visual Studio Code: Stored and organized captured network data for analysis.
- Wireshark: Used for packet capture analysis

## Steps
**1. Install Kali Linux VM.** I had previously installed Linux onto my PC before starting this lab. One of the feautures on Kali Linux is that Wireshark is already installed onto the VM. Then, install Visual Studio Code onto the VM. This was done by downloading the .deb file from the internet.
   
**2. Get familiar with the terminal commands for TCPDump.** The first command used was "tcpdump". This command will be denied by the terminal as it requires admin privileges. Using the command "sudo tcpdump", will prompt a password. Once the password is inputted, the command will be run with elevated privileges. 
   ![sudo tcpdump](https://github.com/user-attachments/assets/94c48730-9356-4cfb-a347-21988be02089)<br>
   
-The next command I ran was "sudo tcpdump -c 10 -#". The "-c 10" argument limits the capture to 10 packets and the "-#" lists the packet captures numerically.<br>
![sudo tcpdump c 10](https://github.com/user-attachments/assets/31565e1d-e04b-4504-9190-2844d3eeb8bc)<br>

-There were a couple of other commands I ran building on tcpdump. One being "sudo tcpdump -c 10 -#XX". The "XX" builds onto the "-#" argument and shows the hexadecimal format for the packet captures.
![sudo tcpdump c 10 XX](https://github.com/user-attachments/assets/949718a4-b0a6-4932-8346-e606364fd445)<br>

-The last command I ran was "sudo tcpdump -c 10 -#XXtttt". The "tttt" portion adds a time format showing the year, month, day, and hour for each of the packet captures.
![sudo tcpdump c 10 XXTTTT](https://github.com/user-attachments/assets/6ec9fbc1-8ef6-449a-9bf2-c400fccd882c)<br>

**3. Start building the logging tool script.**<br>
-If we use the command "sudo tcpdump -#XXtttt host coursera.org" this will only capture all of the incoming and outgoing traffic from coursera.org. This is just an example and a differnt host website will be used later on.<br>
![sudo tcpdump host coursera](https://github.com/user-attachments/assets/559b47e6-af67-4a00-a879-3f61608cd1db)<br>

-The first part in this step is to create a folder where tcpdump will create the files. In this case I named the folder "coursera" on my desktop. Then I ran the command "chmod 777 coursera". This allows third parties to change, modify, and create files in the "coursera" folder. We need this because tcpdump will be creating files containing packet captures.<br>
![image](https://github.com/user-attachments/assets/92a4aa52-0463-4564-8832-f801cac6215a)<br>

-Next, I started up the Visual Studio Code application. From here I created a new file. The location I picked was from my desktop, and I created a folder for the packet captures. In the screenshot below I had already finished up the project so it contains the packet capture files from the finished project.<br>
![image](https://github.com/user-attachments/assets/e919755b-ee11-4405-adb7-6c2ec2c797ac)<br>

-Now the fun part begins, which is building up the script for automated packet captures. Line 1 starts with "#!/bin/bash" to let the system know that it is a script file.<br>
![image](https://github.com/user-attachments/assets/88a54897-d76a-4fe0-8fbe-af16f69525f6)<br>

-Then we add the command line that we used previously into the script.<br>
![image](https://github.com/user-attachments/assets/b0598e75-ec76-4d00-85c4-3e8063b8772b)<br>

-I opened a terminal in the "coursera" folder and ran the command "ls -al" which lists all the files in the coursera folder. Then I ran the command "sudo chmod +x watchdog.sh" which allows everyone to execute the file "watchdog.sh". Then I ran the command "./watchdog.sh" to run that file. The traffic was produced from me opening and refreshing the coursera website.<br>
![image](https://github.com/user-attachments/assets/d075d6bf-53a3-4d6c-bcfd-adfeb0a1cf0f)<br>

**4. Saved captured packets in a dump file.** Here, I added "-w capture.pcap". This writes captured data onto a dump file, in this case our dump file is capture.pcap.<br>
![image](https://github.com/user-attachments/assets/ed527392-a2bc-4c91-b024-665429748454)<br>

-Now if we open the pcap file from Visual Studio Code then it will be unreadable. But if we run the file from the terminal it will display all of the packet captures in a readable format. We use the command "tcpdump -r capture.pcap" and the "-r" reads captured data from dump files as if it was capturing it.<br>
![image](https://github.com/user-attachments/assets/49fca984-10e4-4336-9fa1-430f932df7f8)<br>

-The tool Wireshark works well in conjunction with tcpdump and we can see the captured traffic from there as well. Open Wireshark, then click on "File" in the top left, then click "Open", and then the capture.pcap file will be there. When I open it, the network traffic and the data can be observed from it.<br>
![Wireshark TLS and Encryption](https://github.com/user-attachments/assets/eb8896b7-6eec-4d20-971f-7f829c901576)<br>

**5. Create sequenced dump files.** Any of the previous capture files were deleted to start up new ones. I have gotten rid of the "-c 10", now we are going to develop files to capture passively. I added the "-G" argument which adds a time limit in terms of seconds. Here I am saying that I want to wipeout the capture file and start a new one.<br>
![traffic on wireshark script for it](https://github.com/user-attachments/assets/2f2e6417-a3ce-49dd-9f9a-35e630962876)<br>

-I ran the script in the terminal on the Visual Studio Code. The screenshots below show how it was capturing data, and then 15 seconds later it wipes the data out.<br>
![traffic on wireshark](https://github.com/user-attachments/assets/bd3aa53b-4479-41b3-a897-83803a50ad8f)<br>

![traffic on wireshark packets deleted after 15 seconds](https://github.com/user-attachments/assets/9020a43c-b275-45af-bd28-ca85599d71f1)<br>

-Next, I experimented with the argument "-C" and removed the time limit of "-G". Now, uppercase C is different from the lowercase c argument because it limits the size of the file in megabytes. Instead of limiting the amount of packet captures. We can see now that once a file size reaches around 1 MB, it creates new files after that. Any of these files can be viewed in Wireshark.<br>
![traffic on wireshark script for 1 MG capture file](https://github.com/user-attachments/assets/79ebda7b-7df0-41e3-b02f-4daec5081797)<br>

-This can be built upon and we can create a script that creates packet capture files which will create new files after 10 minutes (with the -G 600 argument), or after 1 MB (with the -C 1 argument).<br>
![traffic on wireshark script for 1 MG or 10 minutes](https://github.com/user-attachments/assets/64bdfa88-9b20-45ba-8bab-84b0f48d7ab8)<br>

**6. Decrypt and analyze captured traffic.** I am going to capture the private and public keys into a capture file done by the browser in our local workstation. Then tcpdump will capture the encrypted data. I am going to use these two to recreate the original unencrypted data.<br>

-I added the command "/usr/bin/google-chrome-stable &" this is what I use to launch my browser. Also by adding the "&" it allows for the script to run lines 4 and 5 together. Otherwise it would just stop at launching Google Chrome. The command "export SSLKEYLOGFILE=" is used to define an environment variable named SSLKEYLOGFILE, which is commonly utilized for debugging encrypted traffic. This variable specifies the file where TLS (Transport Layer Security) session keys will be logged. These keys allow tools like Wireshark to decrypt HTTPS traffic for debugging purposes. Here it creates the file in my "coursera" folder. For demonstration purposes I used the site apod.nasa.gov to capture traffic from there instead. I executed the script watchdog.sh in the Visual Studio Code terminal as shown on the bottom of the next screenshot.<br>
![final code to get http filter running](https://github.com/user-attachments/assets/532ecde0-ced4-4125-85b8-6c8ee03497a2)<br>

-After running the script it opened up Google Chrome. From there I navigated to the apod website and started to create traffic by clicking around the website.<br>
![apod create traffic](https://github.com/user-attachments/assets/a6990768-3f75-4d91-9773-ef29dccfc947)<br>

-To tell Wireshark where the keys are, I went to Edit on the top, then Preferences, then Protocols, then down to TLS. Where it says "(Pre)-Master-Secret log filename", click on browse and then the sslkeys file that was made. This allows us to look at HTTP entries.<br>
![Wireshark preferences](https://github.com/user-attachments/assets/c6875748-6feb-40be-8e83-4faa317d54ab)<br>

-Then I opened the capture.pcap file in Wireshark to observe the traffic. The 129.164.179.22 is the IP address for apod.<br>
![PCAP file](https://github.com/user-attachments/assets/1b26f341-5b4a-45a1-806a-e356c3c68af1)<br>

-Lastly I filtered the HTTP entries in Wireshark to look at them directly. Clicking around the differnt entries, it shows what was being sent back and forth, as well as the encrypted data that was sent. I clicked around a lot of different images on the apod website and that was shown by the network traffic.<br>
![TLS Handshake](https://github.com/user-attachments/assets/b2a4a1ee-a0b8-4c65-980c-3f6a94add8e5)<br>

In the final step I set the environmental variable SSLKEYLOGFILE to the path where I wanted the web browsers to capture the private keys used in SSL encryption. In Wireshark, I set the Protocol TLS Pre-master secret log file to decrypt the encrypted traffic capture.<br>

This project involved using Kali Linux and TCPDump to capture, analyze, and log network traffic while developing critical cybersecurity and scripting skills. After setting up the Kali Linux VM and Visual Studio Code, familiarity with essential TCPDump commands was developed, such as limiting packet captures, applying advanced filters, and recording timestamps. The project progressed to building an automated logging tool in Bash, which facilitated organized and efficient packet capture.

Captured packets were saved in .pcap dump files for analysis using tools like Wireshark, enabling detailed inspection of both encrypted and unencrypted traffic. Advanced functionalities, like creating sequenced dump files based on time intervals or file sizes, enhanced the scope for passive monitoring. Finally, the integration of environment variables such as SSLKEYLOGFILE allowed TLS session keys to be logged, making it possible to decrypt HTTPS traffic for in-depth analysis of web interactions.
