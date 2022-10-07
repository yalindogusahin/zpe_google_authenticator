# zpe_google_authenticator
2-FA for ZPE devices using Google Authenticator

# Configuring the PAM file on Nodegrid

First we need to login as root to the device. For that open console session and type

  shell sudo su -

We need to edit /etc/pam.d/sshd file for adding authentication method

  vi /etc/pam.d/sshd

  auth      required    pam_google_authenticator.so secret=/home/${USER}/.ssh/.google_authenticator nullok

We need to activate ChallengeResponseAuthentication in sshd_config file located in /etc/ssh

  vi /etc/ssh/sshd_config

  ChallengeResponseAuthentication yes

For creating 2FA QR code we need to switch the account that we want to add 2FA. In this case I want to add for admin account.

  sudo su admin

If the admin account doesn't have .ssh folder under /home/admin we need to create that one

  cd /home/admin

   mkdir .ssh

The command for creating QR code is

  google-authenticator -t -Q ANSI -s /home/${USER}/.ssh/.google_authenticator
