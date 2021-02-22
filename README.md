# Day 1 Activity File: Red Team
#
### ELK Server Setup Instructions
#
- As the you attack a web server today, it will send all of the attack info to an ELK server.
* The following setup commands need to be run, before the attack takes place in order to make sure the server is collecting logs.
* Be sure to complete these steps before starting the attack instructions.
#
### Instructions
#
* Double click on the 'HyperV Manager' Icon on the Desktop to open the HyperV Manager.
* Choose the Capstone machine from the list of Virtual Machines and double-click it to get a terminal window.
* Login to the machine using the credentials: vagrant:tnargav
* Switch to the root user with sudo su
#
### Setup Filebeat
#
Run the following commands:
```
filebeat modules enable apache
filebeat setup
```

The output should look like this:

![Filebeat](Images/filebeat.png)
#
### Setup Metricbeat
#
Run the following commands:
```
metricbeat modules enable apache
metricbeat setup
```
The output should look like this:

![Metricbeat](Images/metricbeat.png)
#
### Setup Packetbeat
#
Run the following command:
```
packetbeat setup
The output should look like this:
```
#

Restart all 3 services. Run the following commands:
```
systemctl restart filebeat
systemctl restart metricbeat
systemctl restart packetbeat
```
These restart commands should not give any output:

* Once all three of these have been enabled, close the terminal window for this machine and proceed with your attack.

This how to check if Kibana is running:

![Kibana_check](Images/kibana_check.png)

#

### Attack!

Today, you will act as an offensive security Red Team to exploit a vulnerable Capstone VM.
You will need to use the following tools, in no particular order:

* Firefox
* Hydra
* Nmap
* John the Ripper
* Metasploit
* curl
* MSVenom
#

# Setup

Your entire attack will take place using the Kali Linux Machine.

* Inside the HyperV Manager, double-click on the Kali machine to bring up the VM login window.
* Login with the credentials: root:toor

#

# Instructions

Complete the following to find the flag:

* Discover the IP address of the Linux web server.
 
 ![nmap](images/nmap.png)
 
* Locate the hidden directory on the web server.
   * Hint: Use a browser to see which web pages will load, and/or use a tool like dirb to find URLs on the target site.

![dirb](images/dirb.png)
![Target_Site_Team](images/target_site_team.png)

* Brute force the password for the hidden directory using the hydra command:
   * Hint: You may need to use gunzip to unzip rockyou.txt.gz before running Hydra.

![Gunzip](images/gunzip.png)

* Hint: hydra -l <username> -P <wordlist> -s <port> -f -vV <victim.server.ip.address> http-get <path/to/secret/directory>

![Hydra](images/hydra.png)
![Password](images/ashton_password.png)
![Secret_Folder](images/secret_folder.png)
![Secret_Folder_Notes](images/secret_folder_notes.png)

* Break the hashed password with the Crack Station website or John the Ripper.

![Hash_Result](images/hash_crack_result.png)

* Connect to the server via WebDav.
   * Hint: Look for WebDAV connection instructions in the file located in the secret directory. Note that these instructions may have an old IP Address in them, you will need to use the IP address you have discovered.

![Webdav_Instructions](images/instruction_webdav.png)
![Webdav](images/webdav.png)

* Upload a PHP reverse shell payload.
   * Hint: Try using your scripting skills! MSVenom may also be helpful.

![Multi_Handler_Setup](images/multi_handler_setup.png)
![Msfvenum_Command](images/msfvenum.png)

***Above you created the shell with that command in downloads in the screenshot below you are moving it to the website

![Transferring_Shell](images/transfer_shell.png) 
![Webdav_Website](images/webdav_website.png)

* Execute payload that you uploaded to the site to open up a meterpreter session.

***To activate the session you must click on the Shell.php and go back to the first window where you strted the payload. Correct execution shows up like this:
 
![Status_Meterpreter](images/meterpreter_status.png)

* Find and capture the flag.

![Flag](images/flag.png)

#
