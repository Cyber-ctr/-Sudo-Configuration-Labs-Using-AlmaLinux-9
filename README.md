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
Add User to Sudo Group: Add your user account to the wheel group to grant sudo access:

usermod -aG wheel taptue
Add Sudo Group

Test sudo commands:

sudo fdisk -l
fdisk Own

sudo systemctl status sshd
sshd own

sudo iptables -L
iptables own

Reset Sudo Timer: Run a sudo command, then reset the timer:

sudo fdisk -l
fdisk Own

sudo -k
sudo fdisk -l
fdisk Reset

Edit Sudoers File: Open visudo and search for the Defaults section:

sudo visudo
(Use /Defaults to search within visudo.) Defaults

Disable Global Sudo Timer: In the Defaults section, add or modify the line:

Defaults timestamp_timeout = 0
Save the file and exit visudo. Timeout

Verify Global Timer Disable: Test commands again; you should be prompted for a password each time:

sudo fdisk -l
fdisk Pass

sudo systemctl status sshd
sshd pass

sudo iptables -L
Iptables pass

Set Timeout for Specific User (Lionel): Modify the Defaults line for Lionel:

Defaults:lionel timestamp_timeout = 0
Save and exit visudo. Defaults Lionel

Verify User-Specific Behavior:

Run commands from your own account (taptue):

sudo fdisk -l
sudo systemctl status sshd
sudo iptables -L
fdisk Taptue sshd Taptue iptables Taptue

Switch to Lionel's account and run the same commands:

su - lionel
sudo fdisk -l
sudo systemctl status sshd
sudo iptables -L
exit
fdisk Lionel sshd Lionel iptables Lionel

Check Sudo Privileges: View your sudo privileges:

sudo -l
Check sudo privileges

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











