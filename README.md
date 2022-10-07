# zpe_google_authenticator
2-FA for ZPE devices using Google Authenticator

# Configuring the PAM file on Nodegrid

shell sudo su -

vi /etc/pam.d/sshd

auth      required    pam_google_authenticator.so secret=/home/${USER}/.ssh/.google_authenticator nullok

vi /etc/ssh/sshd_config

ChallengeResponseAuthentication yes

sudo su admin

cd /home/admin

mkdir .ssh

google-authenticator -t -Q ANSI -s /home/${USER}/.ssh/.google_authenticator
