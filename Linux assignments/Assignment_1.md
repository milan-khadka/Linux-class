# Student Name: Milan Kumar Khadka (ICT Robotics)
## Linux Account Setup

First, I created a Microsoft Azure account using our university email address. Once my account was successfully set up, I received $100 in credit, which helped me acquire various tools and resources for learning.

## Create Virtual Machine

Next, I set up a virtual machine to use for learning and projects related to this course. I named the machine "lab-robotics," selected the option for no infrastructure redundancy, and chose the Trusted Launch Virtual Machines security type. I opted for Ubuntu Server 24.04 LTS - x64 Gen2 server with the B series, version 2, specifically Standard_B21s_v2. After completing all the setup steps, I obtained a key and selected the "Connect" option, choosing the native SSH option.
There was a button to copy and execute the SSH command. I copied the key and pasted it into Windows PowerShell, using the generated link to access the Linux virtual machine. This allows us to use Linux on a Windows laptop without installing it.

## Linking my GitHub account to my HAMK email

For the assignment, I created a new repository named "Linux." I also linked my HAMK email as a secondary email for version control.

Some of screenshots while doing the task are as follows:

![alt text](<Screenshot (68).png>) ![alt text](<Screenshot (66).png>) ![alt text](<Screenshot (64).png>) ![alt text](<Screenshot (63).png>) ![alt text](<Screenshot (62).png>) ![alt text](<Screenshot (61).png>) ![alt text](<Screenshot (60).png>) ![alt text](<Screenshot (59).png>) ![alt text](<Screenshot (58).png>)







# Assingment 3 - User management and file system access



### 1. Creating Users Tupu (Using) To create the user tupu, use the following command:

    sudo adduser tupu
This will:

- Create a new user tupu.
- Automatically create the home directory /home/tupu.
- Set the default shell to /bin/bash.
- Prompt for password creation and additional user details.

Tupu (Using) To create the user lupu, use the following command:

    sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu

This will:

- Create the user lupu
- Set the home directory to /home/lupu
- Assign the default shell /bin/bash
- Add lupu to the lupu group

 Set a password for lupu:

    sudo passwd lupu
Hupu (System User) To create a system user hupu with restricted login, use:

    sudo useradd --system --shell /bin/false hupu
This ensures that hupu cannot log in interactively.

### 2. Granting Sudo Privilege Method 1: Using (Recommended) Edit the sudoers file safely:

    sudo visudo 
Add the following lines at the end:

    tupu ALL=(ALL:ALL) ALL
    lupu ALL=(ALL:ALL) ALL
Save and exit.

### Method 2: Adding Users to the Group Alternatively, run:

    sudo usermod -aG sudo tupu
    sudo usermod -aG sudo lupu
Verify with:

    groups tupu
    groups lupu
### Setting Up Shared directory Step 1: Create the directory

    sudo mkdir /opt/projekti
### Step 2: Create and Assign a Group

    sudo groupadd projekti
    sudo usermod -aG projekti tupu
    sudo usermod -aG projekti lupu
### Step 3: Set Directory Ownership

    sudo chown :projekti /opt/projekti
### Step 4: Set Permissions

    sudo chmod 770 /opt/projekti
This allows only tupu and lupu to access and modify files.

### Step 5: Ensure New Files Inherit Group Ownership

    sudo chmod g+s /opt/projekti
This ensures that new files in /opt/projekti inherit the projekti group.

### 4. Verification Check user groups:

    groups tupu
    groups lupu
Check directory permissions:

    ls -ld /opt/projekti
## Output
    drwxrws--- 2 root projekti 4096 Jan 30 18:37 /opt/projekti

# Screenshot

![alt text](<Screenshot (72).png>) 
![alt text](<Screenshot (71).png>)



## Explanation:
  - By creating a common group and applying the setgid bit on the directory, we ensure that all files and directories created within `/opt/projekti` will inherit the group ownership. This setup maintains the desired permission structure where only Tupu and Lupu have access to list, read, and modify files in the directory.

## Submission
- Repository URL: [GitHub Repository]


