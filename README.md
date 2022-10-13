# zpe_google_authenticator
2-FA for ZPE devices using Google Authenticator

# Configuring the PAM file on Nodegrid



> **Warning**

> If you do all configuration via SSH do not close the session before you tested that everything is working,
    else you may lock yourself out. Furthermore consider generating the key file before editing (and therefore applying)
    the PAM configuration.

    

First we need to login as root to the device. For that open console session and type

    shell sudo su -

We need to edit /etc/pam.d/sshd file for adding authentication method

    vi /etc/pam.d/sshd

    auth      required    pam_google_authenticator.so secret=/home/${USER}/.ssh/.google_authenticator nullok
    
> **Warning**

> If you are using RADIUS you need to add this line to /etc/pam.d/s_local

We need to activate ChallengeResponseAuthentication in sshd_config file located in /etc/ssh

    vi /etc/ssh/sshd_config

    ChallengeResponseAuthentication yes
    KbdInteractiveAuthentication yes

For creating 2FA QR code we need to switch the account that we want to add 2FA. In this case I want to add for admin account.

    sudo su admin

If the admin account doesn't have .ssh folder under /home/admin we need to create that one

    cd /home/admin

    mkdir .ssh

The command for creating QR code is

    google-authenticator -t -Q ANSI -s /home/${USER}/.ssh/.google_authenticator
    

    
    
    
# Usefull documentations

    https://wiki.archlinux.org/title/Google_Authenticator
    https://github.com/google/google-authenticator-libpam
        
        
 ![image](https://user-images.githubusercontent.com/103506681/194720918-770cd1f0-f0ef-42f3-8499-efb9cd313ee3.png)

        
