# CYBERSECURITY PROJECT
# Establishing the Lab

**We need two virtual machines: one for testing and another acting as a vulnerable system.  We will use VMware Workstation with Kali Linux installed and deploy Colddbox Easy on Oracle Virtual Box as our target system.**

# What is Coldbox Easy?
**Colddbox Easy is a Wordpress machine that has been designed with an easy level of difficulty. It is an ideal platform for beginners to perform various tests and identify vulnerabilities. This machine is equipped with a range of features that will help you develop your skills and improve your knowledge of cybersecurity. It is an excellent tool to gain hands-on experience in a safe and controlled environment.**

# Installing Kali Linux in VMware Workstation
**Before working on pentesting we need to download :**

**KALI LINUX-** https://www.kali.org/get-kali/#kali-virtual-machines 

# Downloading Colddbox Easy and Oracle Virtual Box
Now that we have Kali Linux installed, it’s time to download Colddbox Easy and Oracle Virtual Box. Follow the links below to download both:

**Download Colddbox: Easy** [https://www.vulnhub.com/entry/colddbox-easy,586/]

**Download Virtual Box:** [https://www.virtualbox.org/wiki/Download_Old_Builds_6_1]

# Procedure of pentesting
**Penetration testing, or pen testing, is a simulated cyberattack conducted by security professionals to identify vulnerabilities in a system or network before malicious actors can exploit them. It involves ethically hacking into a system to assess its security posture and pinpoint weaknesses that need to be addressed.**
<img width="940" height="706" alt="image" src="https://github.com/user-attachments/assets/2f1fbe26-2d58-45c1-b9f5-430b2386d95f" />

# Step 1: Starting Up the Environment
1. Open the terminal in Kali Linux
2. Once in the terminal, we will use the following command to find the IP address of the target machine:
   
               sudo netdiscover

<img width="940" height="456" alt="image" src="https://github.com/user-attachments/assets/554aea22-5593-4b3d-9d0f-9a3348ca19b9" />

# Step 2: Identifying Open Ports and Services
1.If nmap isn't installed, we can install it with

              sudo apt install nmap

<img width="640" height="480" alt="image" src="https://github.com/user-attachments/assets/5b052d14-12ec-445d-9ff1-bba8d87061a4" />


2. With the IP address of the target machine, the next step is to find out the open ports and services available on the machine. Type the command

              nmap -p- -sV 192.168.225.2

3. Press **enter** and wait for the scan to complete
4. It will list all open ports and their associated services on the target IP.
 <img width="1366" height="662" alt="image" src="https://github.com/user-attachments/assets/21b2c246-b687-4a79-9757-ffa996521205" />

NOTE:**Port 80** → Open, running Apache httpd 2.4.18 (Ubuntu) → This means a web server is running.

**Port 4512** → Open, running OpenSSH 7.2p2 (Ubuntu) → This means SSH is accessible on a non-standard port.

It also detected the OS as Linux (Ubuntu) and confirmed the machine is up.
# Step 3: Scanning the Website for Vulnerabilities
1. On your Kali Linux, open Firefox (or your host machine browser, if your VM and host are on the same network).
2. In the address bar, type the target’s IP address:

               http://192.168.225.2
3. Hit Enter.
4. You should see a webpage hosted by Apache (if the web server is running).
<img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/05e34ab1-56e1-4b6a-8f38-749de9604f35" />
<img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/f225eeb8-ee8b-4030-87fc-13e434572ca5" />


# Step 4: WordPress vulnerability scanner 
1. Type the command:

      wpscan --url http://192.168.225.2 --enumerate u
<img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/9ad0ae63-0286-470f-b32f-614528b86959" />

The scanner identified three valid usernames, but we did not know the password. So, in the next step, we will be doing the brute force attack to identify the valid password.

# Step 5: Brute Force Attack
1. We used the WPScanner tool for brute-forcing the password. The command used is:

      wpscan --url http://192.168.225.2 --passwords /usr/share/wordlists/rockyou.txt --usernames c0ldd

<img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/ae2ef513-0ace-45b6-9fac-4a0abc5330db" />

the password is 9876543210.

# Step 6: Enumerate Plugins & Themes
1.      wpscan --url http://192.168.225.2 --enumerate p

   <img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/dcf60ae4-d8d6-4eb3-8235-fa0992b9e848" />

# Uploading a Reverse Shell & Privilege Escalation

# Step 1 — Log in to WordPress Admin
1. Go to:

              http://192.168.225.2/wp-admin
2. Enter the username & password you found from WPScan brute force.

<img width="602" height="292" alt="image" src="https://github.com/user-attachments/assets/f5d6fa8a-160d-4dc0-b5ef-e06ba39e9058" />









