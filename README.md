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






