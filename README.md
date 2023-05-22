# Ubuntu-Server-TLS Setup

# Add user
adduser ubuntu

# Set to super user
usermod -aG sudo ubuntu

# Switch user
sudo su ubuntu

# Add .ssh to ubuntu user
mkdir ~/.ssh
cd ~/.ssh
touch authorized_keys

# generate key in LOCAL
ssh-keygen # then input filename

# Copy .pub content to authorized_keys
# in LOCAL
cat ~/.ssh/filename.pub
# Copy content

# on SERVER
nano ~/.ssh/authorized_keys
# paste ~/.ssh/filename.pub content

# Make ubuntu user sudo without password
sudo visudo
# add this text to the last line then save
ubuntu ALL=(ALL) NOPASSWD:ALL


### SWAP FILES ###

# this setup 4GB of swap file.
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo sh -c 'echo "/swapfile none swap sw 0 0" >> /etc/fstab'
# reboot once
sudo reboot
# SSH back to server and check swapon again.
# check swap file
sudo swapon -s

### Firewall ###

sudo ufw allow 22/tcp     # for ssh
sudo ufw allow 80/tcp     # for http
sudo ufw allow 443/tcp    # only for ssl
sudo ufw show added       # make sure ports that you needed are opened.
# only run this if you are ready
sudo ufw enable


cr. Sakko Sama
https://www.youtube.com/watch?v=UxGriOptHp4
