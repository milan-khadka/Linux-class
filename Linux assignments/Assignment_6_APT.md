# Assignment 6 
**APT Package Management Assignment Documentation**
## Student Name
**Milan Khadka** 
# Part 1: Understanding APT & System Updates.

## 1. Check your system’s APT version:
- **This command displays the installed version of APT on our system.**
### Command:
```
apt --version
```
### Output:
```
apt 2.7.14 (amd64)
```

## 2. Update the package list:
- **Updating the package list is important because it ensures that our system has the latest information about available packages and their versions. This step makes sure that one can install the most current versions and security updates.**

### Command:
```
sudo apt update
```
### Output:
```
Fetched 4083 kB in 1s (5451 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
79 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

## 3. Upgrade installed packages:
### Difference Between Update and Upgrade:

- **Update: Downloads the package information from all configured sources. It does not install or upgrade any packages. Update refreshes the list of available packages and their versions.**

- **Upgrade: Installs the newest versions of all packages currently installed on the system.**

### Command:
```
sudo apt upgrade -y
```
### Output:
```
Running kernel seems to be up-to-date.

Restarting services...
 systemctl restart chrony.service cron.service multipathd.service rsyslog.service ssh.service udisks2.service walinuxagent.service

Service restarts being deferred:
 /etc/needrestart/restart.d/dbus.service
 systemctl restart getty@tty1.service
 systemctl restart networkd-dispatcher.service
 systemctl restart serial-getty@ttyS0.service
 systemctl restart systemd-logind.service
 systemctl restart unattended-upgrades.service

No containers need to be restarted.

User sessions running outdated binaries:
 milan @ session #1: apt[2884], sshd[1003,1118]
 milan @ user manager service: systemd[1008]

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```

## 4. View pending updates (if any):
- **This command lists packages that have updates available but are not yet installed..**
### Command:
```
apt list --upgradable
```
### Output:
```
milan@lab-robotics:~$ apt list --upgradable
Listing... Done
milan@lab-robotics:~$
```
#### The pending updates will vary based on our system's current state and installed packages. so, there is no anything to installed.



# Part 2: Installing & Managing Packages.

## 5.Search for a package using APT:
- **This command Search for a Package or find an image editor**
### Command:
```
apt search image editor
```
### Output / One of the packages from the list: photoflare
```
photoflare/noble 1.6.13-1build2 amd64
  Simple but powerful Image Editor
```


## 6. View package details:
- **Give detailed information about the selected package**
### Command:
```
apt show photoflare
```
### Output:
```
The output will list dependencies such as libraries and other packages required for photoflare to function.
```
### Dependencies Required:
```
Depends: libc6 (>= 2.34), libgcc-s1 (>= 3.3.1), libgomp1 (>= 6), libgraphicsmagick++-q16-12t64 (>= 1.3.26-5~), libqt5core5t64 (>= 5.15.1), libqt5gui5t64 (>= 5.14.1) | libqt5gui5-gles (>= 5.14.1), libqt5network5t64 (>= 5.0.2), libqt5printsupport5t64 (>= 5.0.2), libqt5widgets5t64 (>= 5.10.0), libstdc++6 (>= 4.1.1), qt5-image-formats-plugins
```

## 7. Install the package:
- **Install the Package or Run**
### Command:
```
sudo apt install photoflare -y
```
### Confirmation:
```
The package was successfully installed without any errors.
```

## 8. Check installed package version:
- **This command shows the installed version of the package.**
- **Run**
### Command:
```
apt list --installed | grep photoflare
```
### Output:
```
photoflare/noble,now 1.6.13-1build2 amd64 [installed]
```
### Version Installed:
```
1.6.13
```

# Part 3: Removing & Cleaning Packages.

## 9. Uninstall the package:
- **This command Uninstall the Package.**
- **Package is not fully removed because configuration files may still remain.**

### Command:
```
sudo apt remove photoflare -y
```

### Output / Package Removal Status:
```
The package was successfully removed.
```

## 10.Remove configuration files as well:

- **Run:**
### Command:
```
sudo apt purge photoflare -y
```
### The difference between remove and purge:
- **remove- uninstalls the package but leaves configuration files.**

- **purge- removes the package along with its configuration files.**

## 11. Clear unnecessary package dependencies:
- **This step is important because it removes unused dependencies that were installed automatically but are no longer needed, freeing up disk space.**

- **Run**

### Command:
```
sudo apt autoremove -y
```

## 12. Clean up downloaded package files:

- **This command deletes the local repository of retrieved package files. This frees up disk space as these files can take up a significant amount of space.**

- **In details it removes cached package files (.deb files) from /var/cache/apt/archives/, freeing up disk space.**
- **Run**

### Command:
```
sudo apt clean
```

# Part 4: Managing Repositories & Troubleshooting:

## 13. List all APT repositories:
- **I have noticed that, this file lists the software sources that APT uses to download packages. It includes the URIs for updating and installing packages.**
- **Run**

### Command:
```
cat /etc/apt/sources.list
```

## 14. Add a new repository (example: universe repository):

- **Run**

### Command:
```
sudo add-apt-repository universe
sudo apt update
```
- **The packages found in  universe repository are community-maintained open-source packages.**


## 15. Simulate an installation failure and troubleshoot:

- **Run**

### Command:
```
sudo apt install fakepackage
```

### Error Message:
```
E: Unable to locate package fakepackage
```

### I followed following steps to troubleshoot this issue:
- **Verify the package name is correct**
- **Ensure the repository containing the package is enabled.**
- **Update the package list with ```sudo apt update``` to ensure current package information.**
### Run:
```
sudo apt update
```

# Bonus Challenge (Optional):
- **Use ```apt-mark``` to hold and unhold a package**

### Run:
```
sudo apt-mark hold photoflare
sudo apt-mark unhold photoflare
```
- **Holding a package prevents it from being automatically updated, which is useful for maintaining stability or compatibility with other software.**



  













