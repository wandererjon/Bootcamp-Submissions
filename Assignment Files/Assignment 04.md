## Week 4 Homework Submission File: Linux Systems Administration

### Step 1: Ensure/Double Check Permissions on Sensitive Files

1. Permissions on `/etc/shadow` should allow only `root` read and write access.

    - Command to inspect permissions: 
ls -l /etc/shadow

2. Permissions on `/etc/gshadow` should allow only `root` read and write access.

    - Command to inspect permissions: 
ls -l /etc/gshadow

3. Permissions on `/etc/group` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: 
ls -l /etc/group

4. Permissions on `/etc/passwd` should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: 
ls -l /etc/passwd

### Step 2: Create User Accounts

1. Add user accounts for `sam`, `joe`, `amy`, `sara`, and `admin`.

    - Command to add each user account (include all five users):
    sudo adduser sam
    sudo adduser joe
    sudo adduser amy
    sudo adduser sara
    sudo adduser admin








2. Force users to create 16-character passwords incorporating numbers and symbols.

    - Command to edit `pwquality.conf` file:
 sudo nano /etc/security/pwquality.conf



    - Updates to configuration file:
minlen = 16
dcredit = -1
ocredit = -1
minclass = 3

3. Force passwords to expire every 90 days.

    - Command to to set each new user's password to expire in 90 days (include all five users): 
sudo chage -M 90 joe | sudo passwd -e joe
sudo chage -M 90 sara | sudo passwd -e sara
sudo chage -M 90 amy | sudo passwd -e amy
sudo chage -M 90 admin | sudo passwd -e admin
sudo chage -M 90 sam | sudo passwd -e sam



4. Ensure that only the `admin` has general sudo access.

    - Command to add `admin` to the `sudo` group: 
sudo usermod -aG sudo admin

### Step 3: Create User Group and Collaborative Folder

1. Add an `engineers` group to the system.

    - Command to add group: 
sudo addgroup engineers

2. Add users `sam`, `joe`, `amy`, and `sara` to the managed group.

    - Command to add users to `engineers` group (include all four users):
sudo usermod -aG engineers joe
sudo usermod -aG engineers amy
sudo usermod -aG engineers sara
sudo usermod -aG engineers sam

3. Create a shared folder for this group at `/home/engineers`.

    - Command to create the shared folder: 
sudo mkdir engineers

4. Change ownership on the new engineers' shared folder to the `engineers` group.

    - Command to change ownership of engineer's shared folder to engineer group: 
sudo chown :engineers /home/engineers

5. Add the SGID bit and the sticky bit to allow collaboration between engineers in this directory. 

    - Command to set SGID and sticky bit to shared folder: 
sudo chmod g+s /home/engineers/ 
sudo chmod o+t /home/engineers/

### Step 4: Lynis Auditing

1. Command to install Lynis: sudo apt -y install lynis

2. Command to see documentation and instructions: man lynis

3. Command to run an audit: sudo lynis audit system

4. Provide a report from the Lynis output on what can be done to harden the system.
    - Screenshot of report output: 

![04a](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/d9a7eab4-5247-4780-bd51-3d56b5dc4f01)


### Bonus
1. Command to install chkrootkit: sudo apt -y install chkrootkit

2. Command to see documentation and instructions: man chkrootkit

3. Command to run expert mode: sudo chkrootkit -x

4. Provide a report from the chrootkit output on what can be done to harden the system.



   - Screenshot of end of sample output:
![04b](https://github.com/wandererjon/Bootcamp-Submissions/assets/69092248/0ad2deab-9b92-4223-bb64-468b8bcb6254)

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
