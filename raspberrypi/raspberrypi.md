# Setting Up Raspberry Pi

## Contents
* Install OS
* Enable ssh
* Change User Management
* Add ssh-key for Git
* Commands at Boot

### Install OS
1. Connect microSD card with card reader onto the laptop.

2. Install [Raspbian OS](http://downloads.raspberrypi.org/raspbian_lite/images/).

3. Flash OS to SD card using [Etcher](https://etcher.io/).

### Enable ssh

1. Keep the SD card reader mounted on the laptop.

2. Enter the SD card directory.
   ```bash
   cd /media/user/boot/
   ```

3. Enable ssh.
   ```bash
   touch ssh
   ```

4. Now unmount the SD card from the laptop. Place the SD card into the Raspberry
   Pi along with an ethernet cable.

5. Go to http://192.168.0.1 assuming you have authorization.

6. Find the IP address of your Raspberry Pi.

7. Now connect to the Raspberry Pi.
   ```bash
   ssh pi@192.168.0.x
   ```

8. Default password is raspberry'.

### Change User Management

1. Add user.
   ```bash
   sudo adduser username
   ```

2. Enable sudo priveleges.
   ```bash
   sudo visudo
   ```

   Under '# User privilege specification', append 'username ALL=(ALL:ALL) ALL'.

3. Connect to the Raspberry Pi with your new account.
   ```bash
   ssh username@192.168.0.x
   ```

4. Check you have sudo permissions.
   ```bash
   sudo visudo
   ```

5. Remove the default 'pi' account
   ```bash
   sudo deluser pi
   ```

### Add ssh-key for Git

1. Install git.
   ```bash
   sudo apt-get install git
   ```

2. Generate [ssh-key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).

### Commands at Boot

1. Open up the 'rc.local' file.
   ```bash
   sudo nano /etc/rc.local
   ```

2. Add commands before 'exit 0'.

