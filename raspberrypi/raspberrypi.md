# Setting Up Raspberry Pi

This guide explains how to setup a headless Raspberry Pi. In other
words, it is setting up the Raspberry Pi without a monitor, mouse,
nor keyboard.

## Contents
* Install OS
* Enable ssh
* Change User Management
* Add ssh-key for Git
* Commands at Boot

### Install OS
1. Connect microSD card with card reader onto the laptop.

2. Install [Raspbian OS](http://downloads.raspberrypi.org/raspbian_lite/images/). Use Jesse instead of Stretch for MySQL instead of MariaDB.

3. Flash OS to SD card using [Etcher](https://etcher.io/).


### Enable Wi-Fi on Rasberry Pi

1. Type command `sudo raspi-config`. Go to `Localisation Options`
   and select the US.

2. Enter the SD card directory.
   ```bash
   cd /media/user/boot/
   ```

3. Edit the `wpa_supplicant.conf` file in the `boot` directory. Note
   that this copies `wpa_supplicant.conf` into
   `/etc/wpa_supplicant/wpa_supplicant.conf` on the Raspberry Pi.
   ```bash
   sudo nano wpa_supplicant.conf
   ```


4. Specify the Wi-Fi network to connect to by adding this content into
   the file.
   ```bash
   ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
   update_config=1
   country=US
   network={
       ssid="Wi-Fi Name"
       psk="Password to Wi-Fi"
       key_mgmt=WPA-PSK
   }
   ```

5. If the Wi-Fi connection initially does not work, then `ssh` to
   the Raspberry Pi via Ethernet. The Wi-Fi does not work because
   the Raspberry Pi may be restricted to connect to that specific
   network. It seems like the Raspberry Pi is unable to connect to
   5G networks.

6. When on the Raspberry Pi via command line, enter this command to
   view available networks to connect to.
   ```bash
   sudo iwlist wlan0 scan
   ```

7. To add priority Wi-Fi connections, copy and paste this content
   into the `/etc/wpa_supplicant/wpa_supplicant.conf` file. This is
   useful if you have to connect to the college campus Wi-Fi at
   times. Do note that the machine you `ssh` into must be on the
   same network as you.
   ```bash
   network={
       ssid="HomeOneSSID"
       psk="passwordOne"
       priority=1
       id_str="homeOne"
   }

    network={
        ssid="HomeTwoSSID"
        psk="passwordTwo"
        priority=2
        id_str="homeTwo"
    }
   ```

8. If you do not know the IP address of the Raspberry Pi, you can
   ping it as long as it is on the same Wi-Fi network as your
   laptop.
      ```bash
   ping raspberrypi.local
   ```

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

### Transfer Files via ssh

1. Obtain IP address of Raspberry Pi.

2. Run the below command on the server.
   ```bash
   scp FILE_NAME 192.168.0.xx:/home/user
   ```

### Playing Audio Files on Raspberry Pi

1. Install `omxplayer`.
   ```bash
   sudo apt install omxplayer
   sudo usermod -a -G video $(whoami)
   ```

2. Play the file.
   ```bash
   omxplayer FILE_NAME.mp3
   ```

3. Display all key options during playback.
   ```bash
   omxplayer --keys
   ```

### Change Hostname of the Raspberry Pi

1. Edit the hostname file.
   ```bash
   sudo nano /etc/hostname
   ```

2. Also update the hostname in this other file.
   ```bash
   sudo nano /etc/hosts
   ```

3. Now attempt to `ping` the new hostname.
   ```bash
   ping NEW_HOST_NAME.local
   ```
