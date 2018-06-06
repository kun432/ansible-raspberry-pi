# ansible-raspberry-pi

setting up my raspberry pi 3 (RASPBIAN STRETCH LITE） using ansible.

## Prerequisite

### Install Raspbian Stretch Lite on SD

- Insert SD card into USB card reader and connect to your Mac.
- Format SD card with SD Card Formatter.
- Check your SD card device path.

```
$ diskutil list
/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *32.2 GB    disk2
   1:             Windows_FAT_32 XXX                     32.2 GB    disk2s1
```

- Unmount SD card.

```
$ sudo diskutil umount /dev/disk2s1
```

- Write Raspbian Image to SD card.

```
$ sudo dd if=2018-04-18-raspbian-stretch-lite.img of=/dev/rdisk2 bs=1m

```

- SD will be mounted automatically, Enable SSH in advanced.

```
$ touch /Volumes/boot/ssh
```

- Unmount SD card and eject.

```
$ sudo diskutil umount /dev/disk2s1
```

### 2. Boot your RPi3 and login.

- Connect RPi3 to your network.
- Boot. While booting, Must check your IP address assigned to RPi3.
- SSH RPi3
  - User: pi
  - Password: raspberry

```
$ ssh pi@XXX.XXX.XXX.XXX
pi@192.168.0.138's password:
pi@raspberrypi:~ $
```

### 3. Set up minimum networking setttings.

#### IP address

For networking, I prefer physical interface and fixed IP rather than Wi-Fi and DHCP.

```$ sudo vi /etc/dhcpcd.conf```

```
~~~~~~~~

interface eth0
static ip_address=192.168.0.10/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```
#### Reboot

```
$ reboot
```

## Usage

```
$ git clone https://github.com/kun432/ansible-raspberry-pi.git
```

fix ```hosts``` to be suitable for your environment.

```
$ ansible-playbook -v -i hosts site.yaml --ask-pass -u pi
```