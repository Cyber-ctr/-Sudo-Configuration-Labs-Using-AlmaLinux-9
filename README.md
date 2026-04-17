# Sudo-Configuration-Labs-Using-AlmaLinux-9  

# Overview
This repository contains hands-on labs demonstrating advanced Linux system administration skills on AlmaLinux 9. These labs focus on managing sudo users privileges and configuring sudo users behavior, showcasing practical knowledge of user access control and system security.

# Requirements
* AlmaLinux 9 virtual machine
* Root access or sudo privileges for initial setup
* Basic familiarity with Linux command line

# Lab 1: Assigning Limited Sudo Privileges 

# objective
Create user accounts and assign different levels of sudo privileges to demonstrate granular access control.

# steps

sudo useradd lionel
sudo passwd lionel

sudo useradd katelyn
sudo passwd katelyn

sudo useradd maggie
sudo passwd maggie

Switch to each account to verify creation:
<img width="644" height="351" alt="VirtualBoxVM_4kWqtZzIEh" src="https://github.com/user-attachments/assets/a0274e87-a2c4-4134-82d5-a1b889258ca0" />

2. Edit the Sudoers File: Open the sudoers file with visudo for safe editing:
sudo visudo
<img width="633" height="405" alt="VirtualBoxVM_y4TUrMS2KT" src="https://github.com/user-attachments/assets/42641847-318e-4e00-ab3e-c7047f3582ea" />


3. Enable STORAGE Command Alias:
* Locate the STORAGE alias in the file.
* Uncomment the line by removing the # symbol.

<img width="628" height="396" alt="tLIbOZXWFy" src="https://github.com/user-attachments/assets/5accf9ec-6ef4-4b92-8528-7109d8288a80" />
<img width="639" height="410" alt="3NOIWuIqjr" src="https://github.com/user-attachments/assets/edeeff28-2581-4f97-8c1e-bea032d77801" />


4. Add User Privilege Rules: Append the following rules at the end of the sudoers file:

lionel ALL=(ALL) ALL

katelyn ALL=(ALL) /usr/bin/systemctl status sshd

maggie ALL=(ALL) STORAGE

<img width="637" height="65" alt="7fJHJpwDZ1" src="https://github.com/user-attachments/assets/d4ddd0a1-30ff-47e1-9ec1-bba4d76d40a7" />

Save the file and exit.

5. Verify Lionel's Privileges: Switch to Lionel's account and test commands:

su - lionel

sudo su

exit

sudo systemctl status sshd

<img width="884" height="561" alt="image" src="https://github.com/user-attachments/assets/8363e31c-87f8-4488-9e31-636db07bd56e" />

6. Verify Katelyn's Privileges: Switch to Katelyn's account and test commands:
   su - katelyn
   
   sudo su
   
   sudo systemctl status sshd
   <img width="902" height="493" alt="image" src="https://github.com/user-attachments/assets/ddf6d184-4e93-4271-83fc-683662b3bdf8" />

   sudo systemctl restart sshd

   sudo fdisk -l

   exit

  <img width="1073" height="165" alt="image" src="https://github.com/user-attachments/assets/7b416dd4-1dfc-4680-985f-ee207744394e" />


 7. Verify Maggie's Privileges: Switch to Maggie's account and test commands:
    <img width="975" height="616" alt="image" src="https://github.com/user-attachments/assets/cd482b7f-3149-46cc-94b9-ab997f18cbd7" />


# Lab 2: Disabling the Sudo Timer
# Objective
Configure and disable the sudo password timeout (sudo timer) on AlmaLinux 9 to enhance security by requiring password entry for every sudo command, both globally and for specific users.

# Steps
1.	Log in to the same AlmaLinux virtual machine that you used for the previous lab
This is done by typing the command below in the terminal;
Su – username
2.	At your own user account command prompt, run the following:
sudo fdisk -l
sudo systemctl status sshd
sudo iptables –L
<img width="892" height="564" alt="image" src="https://github.com/user-attachments/assets/20ff0189-9ebb-4815-a898-b5f8628d89e2" />

3.	At your own user account command prompt, run the following:
sudo fdisk -l
sudo -k
sudo fdisk –l
 
<img width="904" height="576" alt="image" src="https://github.com/user-attachments/assets/687c1cf3-50e6-4d27-9000-5f83c47cdfd6" />


4.	Note how the sudo -k command resets your timer, so you will have to enter your password again. Open visudo with the following command:
sudo visudo
The sudo –k command resets the timer, such that at any sudo command being entered, a password is required (Authentication).


5.	In the Defaults specification section of the file, add the following line:
Defaults timestamp_timeout = 0

<img width="975" height="120" alt="image" src="https://github.com/user-attachments/assets/2748f77c-9ade-4e06-a07e-659813db5470" />
Save the file and exit visudo.

6.	Perform the commands that you performed in step 2. This time, you should see that you have to enter a password every time.
 
<img width="975" height="618" alt="image" src="https://github.com/user-attachments/assets/e5e0411b-ed20-4ddf-a411-77bc8d5350ae" />

 
7.	Open visudo and modify the line that you added so that it looks like this, Save the file and exit visudo:
   
Defaults:lionel timestamp_timeout = 0

<img width="881" height="507" alt="image" src="https://github.com/user-attachments/assets/273481b2-ff61-466e-8b12-89f334c770b8" />

 
9.	From your own account shell, repeat the commands that you performed in step 2. Then, log in as Lionel and perform the commands again.

<img width="975" height="609" alt="image" src="https://github.com/user-attachments/assets/5dae58d5-f531-47af-b88b-72e9853daf67" />

 
From the above, we see that when we type in the first command, the system prompts us to input our password after which it doesn’t require authentication for the other commands.

 <img width="1030" height="651" alt="image" src="https://github.com/user-attachments/assets/74bf5750-3b3c-4348-8ab2-1cf34aa0940a" />

From the above we can see that when switched to user lionel, everytime, we type any of the commands in step 2 above, we are prompted by the system to input a password.
9.	View your own sudo privileges by running the following:

sudo –l

<img width="975" height="212" alt="image" src="https://github.com/user-attachments/assets/c26c13ff-ac82-4f2a-bc28-3799849987f4" />
 


# Key Learnings
Configuring granular sudo privileges enhances system security by limiting user access.
Understanding sudoers file syntax and command aliases.
Managing sudo timer for different security requirements, including global and per-user settings.
Practical user account management and group assignments in Linux environments.
Resetting sudo sessions and verifying privilege configurations.
# Technologies Used
AlmaLinux 9
Sudo configuration and visudo
Systemctl for service management
User management tools (useradd, passwd, usermod)
Iptables for firewall management
This project demonstrates proficiency in Linux system administration, particularly in access control, security configuration, and user privilege management.











