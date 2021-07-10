- Download image from [[https://archlinux.org/download/]]
- Mount 64-bit version
- Install defaults
- ping to check network, eg `ping google`
- ctrl+c to stop ping process
- clear to stop it

- check disks with `sfdisk -l`, just to check how much space there is

### partition the hard disk
- type `cfdisk`, click enter
- you will see gpt, dos, sgi and sun. select sun
- on the new screen click enter and type the size of the partition.
- For this VM I allocated around 31GB. Main is 15GB. If you allocated 20GB for this, give it 10GB, if more, allow for more. You need 3 partition overall: main, swap and logical. swap should be around the amount of ram you are giving your VM. logical should be the rest. My sizes are 15 main, 8 Swap, 8 Logical.
- After you type the size, click enter, followed by select primary, followed by Bootable type by pressing enter on it. After that go to write, click enter, when prompted, write out yes and click again enter
- Now move down to free space with the cursor, down arrow
- enter and write in the size for your swap. swap size guide can be easily found online; TL:DR: swap == RAM up to 8GB.
- select primary and make sure to go to write, spell out again yes and enter
- follow the same steps for the logical part with the remainder of the space
- select `quit`
- and clear this mess

### Formating the new partitions
- type `mkfs.ext4 /dev/sda1` and hit enter
- type `mkfs.ext4 /dev/sda3`
- check the text, if its a wall of text with a creating files and filesystems, superblock text, everything went well. If you get error, not found or something else, type again `cfdisk` and make sure you wrote it, if on the open window you only see dev/sda1 and no swap size and name nor logical size and name, you didn't click on write and spelled out yes.
- type `mkswap /dev/sda2`
- activate swap by writting `swapon /dev/sda2`
- `clear` it
- mount it with `mount /dev/sda1 /mnt`
- followed by `mkdir /mnt/home` which should create the home directory
- and `mount /dev/sda3 /mnt/home`

### PacMan Setup
- run `pacstrap /mnt base base-devel` in the terminal
- installation will take a few moments
- after it is complete run `genfstab /mnt>> /mnt/etc/fstab`
- nothing will happen, no text should display
- run `arch-chroot /mnt /bin/bash`, this command switches it to chroot,
### set up language & time zone
- run `nano /etc/locale.gen`, if this returns command not found, run `pacman -S nano` to install nano, and run the previous command again. it should open up a text file to configure the language.
- go down and select the one applicable, if in US, go down and find en_US.UTF-8 UTF-8, delete the # in front of it, and save the file (ctrl+x, y, enter)
- once that is saved, activated it by running `locale-gen`
- now we can generate the conf file for the language
- run `nano /etc/loacel.conf`
- it will open an empty text file, type in `LANG=en_US.UTF-8`, save it (ctrl+x, Y, enter).
- now it's time to set up timezone, type in `ls /usr/share/zoneinfo` to see the list of all the zones in the world. the list is not complete, to get an accurate list visit [[https://en.wikipedia.org/wiki/List_of_tz_database_time_zones]]
- currently living in Idaho, therefore my timezone was America/Boise.
- the next line was `ln -s /usr/share/zoneinfo/America/Boise /etc/localtime`. Remember to update the last part of this line with your correct location.
- set the time standard using `hwclock --systohc --utc`. this should sync the hardware clock. "should".
### password and host name
- set a new password by typing `passwd`
- current password is ***************
- to add a hostname for the network type `nano /etc/hostname`
- type in the name of the server, save it (nano-save-sequence)
- type `systemctl enable dhcpcd`. apparently this will be started on next bootup and automatically get an IP address.
- error `failed to enable unit, unit dhcpcd.service does not exist` if you see this, it means the dhcpcd package was not installed. to fix run `pacman -S dhcpcd` and follow up with the previous command.
