# Linux

- [Linux](#linux)
  - [Books and articles](#books-and-articles)
  - [Ubuntu](#ubuntu)
    - [Ubuntu Midi keyboard](#ubuntu-midi-keyboard)
    - [Recording screen + audio](#recording-screen--audio)
  - [Tools](#tools)
    - [Onedrive sync for linux](#onedrive-sync-for-linux)
    - [Taskwarrior - a todo list on the commandline](#taskwarrior---a-todo-list-on-the-commandline)
  - [Bash shell programming](#bash-shell-programming)
  - [ZSH](#zsh)
  - [SMB drive mappings](#smb-drive-mappings)
  - [Ubuntu key shortcuts](#ubuntu-key-shortcuts)
  - [Installing Packages](#installing-packages)
    - [Apt and apt-get](#apt-and-apt-get)
    - [Using Debian package manager](#using-debian-package-manager)
    - [Checking Kernel and system info](#checking-kernel-and-system-info)
    - [Checking version of linux](#checking-version-of-linux)
    - [Checking Hardware Configuration](#checking-hardware-configuration)
  - [Checking network usage](#checking-network-usage)
  - [User Stuff](#user-stuff)
  - [SSH tips](#ssh-tips)
    - [links about using ssh agent & security](#links-about-using-ssh-agent--security)
      - [Some other articles about ssh login without password (NB - ssh agent solution is useful)](#some-other-articles-about-ssh-login-without-password-nb---ssh-agent-solution-is-useful)
  - [Bash profile & History](#bash-profile--history)
  - [Cleaning Snaps](#cleaning-snaps)
  - [FStab](#fstab)
  - [Managing Swap space](#managing-swap-space)
  - [Managing /var space](#managing-var-space)
  - [Setting java version](#setting-java-version)
  - [Using Screen](#using-screen)
    - [Alternative to screen for an already running process](#alternative-to-screen-for-an-already-running-process)
  - [filesys overview](#filesys-overview)
  - [Small Linux installs](#small-linux-installs)
    - [**Creating a boot USB key**](#creating-a-boot-usb-key)
    - [Beautiful icon sets](#beautiful-icon-sets)
  - [SED AWK](#sed-awk)
    - [SED Stuff](#sed-stuff)
      - [Simple SED examples](#simple-sed-examples)
      - [SED - Adding stuff to the end of the line](#sed---adding-stuff-to-the-end-of-the-line)
      - [Miscellaneous SED stuff](#miscellaneous-sed-stuff)
    - [AWK Stuff](#awk-stuff)
  - [Annoying repeated - "System program problem detected" messages](#annoying-repeated---system-program-problem-detected-messages)
  - [Terminal Commands](#terminal-commands)
    - [Moving and copying files](#moving-and-copying-files)
    - [Checking number of CPUs - lscpu](#checking-number-of-cpus---lscpu)
    - [SCP & cp](#scp--cp)
    - [Linux IP address](#linux-ip-address)
    - [Monitoring processes - top, vmstat, sysstat](#monitoring-processes---top-vmstat-sysstat)
    - [top cheatsheet](#top-cheatsheet)
    - [tar](#tar)
    - [mkdir creating directories](#mkdir-creating-directories)
    - [ifconfig is dead, use ip instead](#ifconfig-is-dead-use-ip-instead)
    - [Disk Usage, Disk Free space](#disk-usage-disk-free-space)
      - [NCDU - disk space usage checker](#ncdu---disk-space-usage-checker)
      - [du and df](#du-and-df)
    - [netstat](#netstat)
    - [Lookup hostname from IP address](#lookup-hostname-from-ip-address)
    - [File Permissions](#file-permissions)
    - [Find utility](#find-utility)
    - [List files in directories in a Tree](#list-files-in-directories-in-a-tree)
    - [Word Counts - find number of files in dir](#word-counts---find-number-of-files-in-dir)
    - [Grep](#grep)
      - [**Other options**](#other-options)
    - [Grep to find text within files](#grep-to-find-text-within-files)
      - [Grep patterns](#grep-patterns)
    - [System Suspend from commandline](#system-suspend-from-commandline)
    - [Ubuntu on a netbook](#ubuntu-on-a-netbook)
    - [Docker Installs for Linux - Ubuntu](#docker-installs-for-linux---ubuntu)
      - [Example of the output from the hello world container](#example-of-the-output-from-the-hello-world-container)
    - [Mini Cheatsheet](#mini-cheatsheet)
    - [Learning Docker](#learning-docker)
    - [Docker Compose](#docker-compose)
    - [XHCI issues](#xhci-issues)
    - [Screenshots](#screenshots)
  - [List of Linux Topics](#list-of-linux-topics)
  - [Vim Cheatsheet](#vim-cheatsheet)
    - [General text manipulation](#general-text-manipulation)
  - [Less Cheatsheet](#less-cheatsheet)

## Books and articles

- <https://linuxcommand.org/index.php> and the pdf version <https://netcologne.dl.sourceforge.net/project/linuxcommand/TLCL/19.01/TLCL-19.01.pdf>
- Gamifying linux learning - <https://www.reddit.com/r/linux4noobs/comments/luzgz9/looking_for_websites_like_overthewire_to_learn/>

## Ubuntu

- <https://itsfoss.com/things-to-do-after-installing-ubuntu-18-04/>
- How to make an OS with linux and Raspberry PI -
    <https://s-matyukevich.github.io/raspberry-pi-os/>

### Ubuntu Midi keyboard

- Super Basic HowTo Connect a MIDI Keyboard -
    <https://ubuntuforums.org/showthread.php?t=1303306>

### Recording screen + audio

- Discussion on LinuxMint - <https://forums.linuxmint.com/viewtopic.php?t=350180>
- OBS tool <https://obsproject.com/download>

## Tools

### Onedrive sync for linux

- <https://www.maketecheasier.com/sync-onedrive-linux/>
- <https://www.linuxuprising.com/2020/02/how-to-keep-onedrive-in-sync-with.html>
- Simple with RClone - <https://www.linuxuprising.com/2018/07/how-to-mount-onedrive-in-linux-using.html>

My Notes:
  - Reading the pages above I went to the onedrive client github and followed the install instructions
    - <https://github.com/abraunegg/onedrive/blob/master/docs/INSTALL.md>
      
```bash      
  sudo apt install build-essential
  sudo apt install libcurl4-openssl-dev
  sudo apt install libsqlite3-dev
  sudo apt install pkg-config
  sudo apt install git
  sudo apt install curl
  curl -fsS https://dlang.org/install.sh | bash -s dmd

  # For notifications
  sudo apt install libnotify-dev
```

  - Following the dependency installs I followed the compile section
    - Activate dmd following the output of the install from above

```bash
  Run `source ~/dlang/dmd-2.098.1/activate` in your shell to use dmd-2.098.1.
  This will setup PATH, LIBRARY_PATH, LD_LIBRARY_PATH, DMD, DC, and PS1.
  Run `deactivate` later on to restore your environment.

```
  - After that the make etc. worked and I could authorize the app with onedrive
  - onedrive --synchronize --single-directory 'LinuxSync'


### Taskwarrior - a todo list on the commandline

- <https://taskwarrior.org/docs/>

## Bash shell programming

- dedicated page:
    <http://www.iamdarren.net/wikidc/doku.php?id=development:scripts>
- Links to some nice resources for Shell and commandline -
    <https://www.reddit.com/r/linuxquestions/comments/ewbl9f/explainshellcom_is_an_awesome_resource/>
- Really NICE SITE TO BREAKDOWN COMMANDS AND EXPLAIN THEM:
    <https://explainshell.com/>
- PDF with a LOT of different resources -
    <https://www.usenix.org/sites/default/files/conference/protected-files/lisa19_maheshwari.pdf>

## ZSH

- <https://medium.com/@harrison.miller13_28580/bash-vs-z-shell-a-tale-of-two-command-line-shells-c65bb66e4658>
- <https://www.howtogeek.com/362409/what-is-zsh-and-why-should-you-use-it-instead-of-bash/>
- Nice getting started guide - <https://www.sitepoint.com/zsh-tips-tricks/>
- <https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH>

- <https://github.com/derailed/k9s>
- <https://webinstall.dev/>
- <https://github.com/romkatv/powerlevel10k#oh-my-zsh>
- <https://github.com/ohmyzsh/ohmyzsh>
- Also install some extra fonts - <https://github.com/powerline/fonts>
- Productivity plugins - <https://travis.media/top-10-oh-my-zsh-plugins-for-productive-developers/#20210719-json>

### powerline10k

- following guide in readme - https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k

```bash
# from mint machine
darren@darren-iMac-Mint:~$ zsh
                                                                                
New config: ~/.p10k.zsh.
Backup of ~/.zshrc: /tmp/.zshrc.JZtb3qunUJ.

See ~/.zshrc changes:

  diff /tmp/.zshrc.JZtb3qunUJ ~/.zshrc

```


## SMB drive mappings

This is where an SMB share is mapped when you've added it in
Nautilus/Filemanager: /\$XDG_RUNTIME_DIR/gvfs

## Ubuntu key shortcuts

```bash
    à - AltGr ` a
    è - AltGr ` e
    é - AltGr ' e

    € - AltGr = e
    ç - AltGr , c
    ê - AltGr Shift+> e
```

- Full list - <https://help.ubuntu.com/community/GtkComposeTable>

## Installing Packages

### Apt and apt-get

Apt command was added by linux in 2014 to combine commonly used features
of apt-get and apt-cache

- apt-get: installing, upgrading and removing software packages.
- apt-cache: search for new packages.

Can possibly need to execute with sudo

```bash

# installing/removing a particular package
sudo apt install nmap
sudo apt remove nmap
sudo apt purge nmap

# Updating package lists and then upgrading them. Can also upgrade individual packages by name
sudo apt update
sudo apt upgrade

# List all packages, grep for a particular package. Version is also displayed.
$ apt list
$ apt list | grep <packageName>
$ apt list --installed
$ apt list --upgradeable

# Search for package in available packages, show information about a package - dependencies, installation size, package source
$ apt search package_name
$ apt show package_name

```

- Apt tutorial page -
    <https://phoenixnap.com/kb/how-to-use-apt-get-commands>,
- Another one - <https://linuxize.com/post/how-to-use-apt-command/>

### Using Debian package manager

```bash
# seeing a list of installed packages
dpkg -l | less
dpkg -l <packageName>

#To check whether a package is installed or not:

dpkg -l {package_name}
dpkg -l vlc
dpkg -l | grep vlc

Show the location where the package is installed. The "-S" (capital S) stands for "search"

sudo dpkg -S {package_name}
sudo dpkg -S skype


# Installing a local package 
sudo dpkg -i package_file.deb

```

### Checking Kernel and system info

```bash
uname -a # for all information regarding the kernel version
uname -r # for the exact kernel version
lsb_release -a # for all information related to the Ubuntu version,
lsb_release -r # for the exact version
sudo fdisk -l # for partition information with all details.

dpkg -l | grep linux-image # displays all installed kernels
dpkg -l | tail -n +6 | grep -E 'linux-image-[0-9]+'

apt-mark showmanual 'linux-image-.*' # show manually installed kernels
apt-mark showauto 'linux-image-.*'   # show auto installed kernels

sudo apt --purge autoremove # remove unused old kernels (only removes auto installed kernels I think)

```

- Information on cleaning up old kernels -
    <https://help.ubuntu.com/community/RemoveOldKernels>
- <https://www.calazan.com/how-to-set-an-older-kernel-version-as-the-default-in-grub-during-bootup-ubuntu-12-04/>

- Updating kernel via grub reboot
- sudo grub-reboot "Advanced options for Ubuntu>Ubuntu, with Linux 4.2.0-16-generic"
- sudo reboot

### Checking version of linux 

- <https://stackoverflow.com/questions/13036048/how-do-i-identify-the-particular-linux-flavor-via-command-line>

```bash
# Get the initial flavour
cat /proc/version

# Then followup with specific commands

# Red Hat for example
cat /etc/redhat-release

# Debian
cat /etc/debian_version

# or in general :
cat /etc/*-release
# Also you could use the following command
cat /etc/issue
```

### Checking Hardware Configuration

lshw command for checking configuration

- <https://linux.die.net/man/1/lshw>

> lshw is a small tool to extract detailed information on the hardware
> configuration of the machine.
>
> It can report exact memory configuration, firmware version, mainboard
> configuration, CPU version and speed,
>
> cache configuration, bus speed, etc. on DMI-capable x86 or IA-64
> systems and on some PowerPC machines (PowerMac G4 is known to work).

- Checking RAM Slots

```bash
sudo lshw -class memory

# Results look like this for 2 RAM slots (Banks) which are both used:

    *-memory
         description: System Memory
         physical id: 4d
         slot: System board or motherboard
         size: 16GiB
       *-bank:0
            description: SODIMM DDR4 Synchronous Unbuffered (Unregistered) 2400 MHz (0.4 ns)
            product: HMA81GS6AFR8N-UH
            vendor: Hynix Semiconductor (Hyundai Electronics)
            physical id: 0
            serial: 2C9D672E
            slot: DIMM A
            size: 8GiB
            width: 64 bits
            clock: 2400MHz (0.4ns)
       *-bank:1
            description: SODIMM DDR4 Synchronous Unbuffered (Unregistered) 2400 MHz (0.4 ns)
            product: HMA81GS6AFR8N-UH
            vendor: Hynix Semiconductor (Hyundai Electronics)
            physical id: 1
            serial: 2C9D6723
            slot: DIMM B
            size: 8GiB
            width: 64 bits
            clock: 2400MHz (0.4ns)

```

## Checking network usage

```bash
# See what process send/receives most packets
netstat -anp --inet
```

## User Stuff

- Checking user groups - <https://www.cyberciti.biz/faq/which-groups-do-i-belong-to/>
  - ``` $ groups ```
  - ``` $ whoami ```

## SSH tips

- Using ssh-add to keep ssh passphrase in session - <https://kb.iu.edu/d/aeww>
- ssh academy - ssh, keygen etc. - <https://www.ssh.com/academy/ssh>
  - ssh Copy-ID to add ssh keys to authorized keys - <https://www.ssh.com/academy/ssh/copy-id#how-ssh-copy-id-works>

### links about using ssh agent & security

- <https://www.commandprompt.com/blog/security_considerations_while_using_ssh-agent/>
- <https://stackoverflow.com/questions/18880024/start-ssh-agent-on-login/>
- <https://linux.101hacks.com/unix/ssh-agent/>
- <https://stackoverflow.com/questions/2205282/ssh-agent-and-crontab-is-there-a-good-way-to-get-these-to-meet/>
- <https://stackoverflow.com/questions/24495395/using-cron-with-ssh-keys/>
- This one looks promising for a fully programatic way to do it by handling the ssh agent stuff on and off - <https://www.akadia.com/services/ssh_agent.html>
- <https://stackoverflow.com/questions/869589/> why-ssh-fails-from-crontab-but-succedes-when-executed-from-a-command-line

#### Some other articles about ssh login without password (NB - ssh agent solution is useful)

- <https://stackoverflow.com/questions/1595848/configuring-git-over-ssh-to-login-once>
- talks about keychain and -K option for restarts - <https://stackoverflow.com/questions/21095054/ssh-key-still-asking-for-password-and-passphrase>
- <https://stackoverflow.com/questions/18880024/start-ssh-agent-on-login>
- <https://stackoverflow.com/questions/12033249/ssh-agent-forwarding-inside-cron-jobs>

## Bash profile & History

- <https://www.shellhacks.com/tune-command-line-history-bash/>
  - Tune the number of lines kept, when it gets written (end of session or immediately)

## Cleaning Snaps

- <https://superuser.com/questions/1310825/how-to-remove-old-version-of-installed-snaps>
- Also here some tips for managing the snaps:
    <https://www.linuxuprising.com/2019/04/how-to-remove-old-snap-versions-to-free.html>

## FStab

The configuration file /etc/fstab contains the necessary information to
automate the process of mounting partitions.

- Mounting fstab without reboot -
    <https://www.shellhacks.com/remount-etc-fstab-without-reboot-linux/>

## Managing Swap space

- swap file instead of partition - <https://linuxize.com/post/create-a-linux-swap-file/>
- Also here with some info about using dd not fallocate - <https://www.howtogeek.com/455981/how-to-create-a-swap-file-on-linux/>
- And from the Ubuntu docs - <https://help.ubuntu.com/community/SwapFaq#How_much_swap_do_I_need.3F>

```bash
# Commands to use - NB I have more space on /home than elsewhere but can put anywhere

# Use ONE of the following to create the swap file - I used second way
sudo fallocate -l 10G /home/swapfile # this is the quick and easy way
sudo dd if=/dev/zero of=/home/swapfile bs=1024 count=10485760 # this is more portable

# setup the swap file for use (permissions to root for using it)
sudo mkswap /home/swapfile
sudo chmod 600 /home/swapfile
sudo swapon /home/swapfile

# Add to fstab to make the change permanent
sudo vim /etc/fstab
#Add this line
/home/swapfile swap swap defaults 0 0
```

## Managing /var space

- Clean way is to correctly organise at install :) but otherwise can resize the logical volume
  - <https://www.digitalocean.com/community/tutorials/how-to-use-lvm-to-manage-storage-devices-on-ubuntu-18-04> as a starting point
- For docker you can use a configuration to point to another storage location (todo - exapand on this point)
- Other way which is much simpler is to create a softlink to a directory on another volume

```bash
sudo systemctl stop snapd.service
sudo mv /var/lib/snapd /home/snapd
sudo ln -s /home/snapd /var/lib/snapd
sudo systemctl start snapd.service
```

NB THIS DOESN'T work for SNAPS :(

- Some suggestions here: <https://askubuntu.com/questions/1029562/move-snap-packages-to-another-location-directory>
  - This I have used and it works very well.
- <https://forum.snapcraft.io/t/where-is-a-snap-stored-and-how-can-i-change-that/3194/4>

script from the above askubuntu solution for mount --point

```bash
##############################################################################
# Take Care this section may break the System !!!
##############################################################################
##Move snap folder to Home instead of root.
#Create the directory : you can change the location
mkdir /home/$USER/snap/snapd

#Copy the data
sudo rsync -avzP /var/lib/snapd/  /home/$USER/snap/snapd/

#Do backups
sudo mv /var/lib/snapd /var/lib/snapd.bak
sudo cp /etc/fstab /etc/fstab.bak

#Change fstab (Change $USER with your name or change the path totally)
echo "/home/$USER/snap/snapd /var/lib/snapd none bind 0 0" | sudo tee -a /etc/fstab

#remount fstab Or reboot.
sudo mkdir /var/lib/snapd
sudo mount -a

if ls  /var/lib/snapd/ | grep snaps
then
    echo "Re-mounting snapd folder is done successfully. !!!!"
    sudo rm -rf /var/lib/snapd.bak
else
    echo "WARNING : Re-mounting snapd folder failed, please revert !!!!! "
    echo "WARNING : Re-mounting snapd folder failed, please revert !!!!! "
    echo "WARNING : Re-mounting snapd folder failed, please revert !!!!! "
    echo "WARNING : Re-mounting snapd folder failed, please revert !!!!! "
    echo "WARNING : Re-mounting snapd folder failed, please revert !!!!! "

    # Trying to revert automatically
    sudo cp /etc/fstab.bak /etc/fstab
```

## Setting java version

```bash
sudo update-alternatives --display java
sudo update-alternatives --config java
```

I followed this tuto for installing java + setting the JAVA_HOME <https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04>

it set JAVA_HOME in /etc/environment which updates for ALL users of the system which isn't necessarily the right way :).

```bash
# Searching for JAVA_HOME setting
$ grep JAVA_HOME  ~/.bashrc_custom ~/.bash_login ~/.profile ~/.bashrc
$ grep JAVA_HOME /etc/environment /etc/bash.bashrc /etc/profile.d/* /etc/profile

...Found it in /etc/environment

```

## Using Screen

- <https://linuxize.com/post/how-to-use-linux-screen/>
- User Manual <https://www.gnu.org/software/screen/manual/screen.html>

```bash
# Useful commands

- On the command prompt, type screen.
- Run the desired program.
- Use the key sequence Ctrl-a + Ctrl-d to detach from the screen
    session.
- Reattach to the screen session by typing screen -r.

# Create new window 0-9

- Ctrl+a c Create a new window (with shell)
- Ctrl+a " List all window
- Ctrl+a 0 Switch to window 0 (by number )
- Ctrl+a A Rename the current window

# Navigating

- Ctrl+a n switch to next window
- Ctrl+a p switch to previous window

- Ctrl+a S Split current region horizontally into two regions
- Ctrl+a | Split current region vertically into two regions
- Ctrl+a tab Switch the input focus to the next region
- Ctrl+a Ctrl+a Toggle between the current and previous region
- Ctrl+a Q Close all regions but the current one
- Ctrl+a X Close the current region

# detach and reattach

- Ctrl+a d - detach from Linux Screen Session
- screen -r - resume screen session
- screen -r 10835 - resume for screen session 10835 (see screen -ls
    below)

# list all screens running on the machine

- screen -ls

```

### Alternative to screen for an already running process

- <https://serverfault.com/questions/34750/is-it-possible-to-detach-a-process-from-its-terminal-or-i-should-have-used-s>

```bash
# How-to:
  # Ctrl+z to interrupt, 
  bg #to put in background, 
  jobs # to see job number, 
  disown %<jobNumber> # get the <jobNumber> value from jobs command
```  

## filesys overview

- <https://opensource.com/life/16/10/introduction-linux-filesystems>

## Small Linux installs

Some small Linux installs for old computers - less than 1GB ram needed.

- Puppy Linux - create a Live CD, then can install on USB stick and
    use on any computer
- Zenix - everything fits on USB live stick

**UNetBootIn** Utility for creating USB live sticks for Linux distros
The Mac version has an annoying bug where you need to do an fdisk on the
usb stick after formatting but before creating your install in order to
activate the partition.

- <http://perpetual-notion.blogspot.fr/2011/08/unetbootin-on-mac-os-x.html>

### **Creating a boot USB key**

- Using dd to flash an iso to a USB key -
    <https://medium.com/@tbeach/use-unix-dd-command-to-os-bootable-on-usb-drive-6671945d95a6>

### Beautiful icon sets

- <https://github.com/EliverLara/candy-icons>

## SED AWK

- [Explanation of SED vs AWK](https://www.makeuseof.com/tag/sed-awk-learn/)

### SED Stuff

- SED documentation - <http://www.tldp.org/LDP/Bash-Beginners-Guide/html/chap_05.html>
- Better SED examples -
  - [Grymoire tutorial](https://www.grymoire.com/Unix/Sed.html#uh-53)
  - [GNU SED manual](https://www.gnu.org/software/sed/manual/sed.html)
    - Examples - <https://www.gnu.org/software/sed/manual/sed.html#Joining-lines>
  - <https://fabianlee.org/2018/10/28/linux-using-sed-to-insert-lines-before-or-after-a-match/>

#### Simple SED examples

```bash
# Delete everything between BEGIN and END lines for all *.txt files, creating a backup .bak for each one and modifying the original
sed -i.bak '/BEGIN/,/END/d' *.txt

# same thing with another string
sed -i.bak2 '/EditStuff/,/EditStuffFinish/d' *.err
```

#### SED - Adding stuff to the end of the line

- <https://stackoverflow.com/questions/15978504/add-text-at-the-end-of-each-line>

```bash
# Finds end of line with $, then adds ":80" to it
sed -n 's/$/:80/' ips.txt > new-ips.txt
```

#### Miscellaneous SED stuff

- Special Chars - <https://stackoverflow.com/questions/43108359/how-to-remove-all-special-characters-in-linux-text>
- Print previous line before match - <https://unix.stackexchange.com/questions/206886/print-previous-line-after-a-pattern-match-using-sed>
- Windows carriage return ^M in files - <https://superuser.com/questions/194668/grep-to-find-files-that-contain-m-windows-carriage-return>

### AWK Stuff

- AWK documentation - <http://www.tldp.org/LDP/Bash-Beginners-Guide/html/chap_06.html>

## Annoying repeated - "System program problem detected" messages

System program problem detected gets displayed repeatedly after there
has been a crash. Mostly its okay to delete the reports

```bash
# See the list of crash reports ll /var/crash/

total 988 drwxrwsrwt 2 root whoopsie 4096 Jan 17 15:55 ./ drwxr-xr-x 15
root root 4096 Jul 25 2018 ../ -rw-r\--r\-- 1 kernoops whoopsie 2648 Jan
15 11:30 linux-image-4.18.1-041801-generic.220862.crash -rw-r\-\-\-\-- 1
root whoopsie 28316 Jan 17 10:57
\_usr_bin_landscape-package-changer.0.crash -rw-r\-\-\-\-- 1 dcostello
whoopsie 967043 Jan 17 15:55 \_usr_bin_onedrive.1000.crash

# Remove if it's okay
sudo rm /var/crash/*

```

## Terminal Commands

### Moving and copying files

```bash
# Move multiple files/directories to a directory
mv -t <DESTINATION> <source1> <source2> ......
```

### Checking number of CPUs - lscpu

```bash
$ lscpu

# example output
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              8
On-line CPU(s) list: 0-7
Thread(s) per core:  2
Core(s) per socket:  4
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               142
Model name:          Intel(R) Core(TM) i7-8650U CPU @ 1.90GHz
Stepping:            10
CPU MHz:             3595.397
CPU max MHz:         4200.0000
CPU min MHz:         400.0000
BogoMIPS:            4224.00
Virtualization:      VT-x
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            8192K
NUMA node0 CPU(s):   0-7
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp flush_l1d

```

### SCP & cp

- SCP examples -
    <https://haydenjames.io/linux-securely-copy-files-using-scp/>

```bash
# Recursive copy
cp -r <pathToTarget> <pathToDest>

# Copy multiple named files
cp ./{File1,File2,File3} <pathToDest>
```

### Linux IP address

ifconfig when root (or \$cd /sbin/ then \$./ifconfig if not) or \$curl
whatismyip.org

### Monitoring processes - top, vmstat, sysstat

- Sysstat - suite of tools to monitor
    <https://github.com/sysstat/sysstat>
- top command
- vmstat - <http://man7.org/linux/man-pages/man8/vmstat.8.html>

```bash
# TOP - log out to a file in batch mode -n iterations -d interval in secs -o order by field -b batch mode
top -n 10 -d 2 -o %CPU -b \> \~/dcTOP.txt

# To limit output can run top once interactively, limit number of
processes with n then W to write a user config file

# VMSTAT - gives memory and cpu info - the command below will run it with a timestamp, format the memory in MB and repeat every 30s for 500 repetitions (enough for 2hrs run)
vmstat -t -S M 30 500 2>&1 | tee vmstats.txt
```

### top cheatsheet

- After running top command:
  - Shift+m - Sort processes by memory usage
  - Shift+f to enter the interactive menu
    - press the up or down arrow until the %MEM choice is
            highlighted
    - press s to select %MEM choice
    - press enter to save your selection
    - press q to exit the interactive menu
    - Specify the sort order on the command line
      - top -o %MEM

### tar

```bash
# Tar and zip
$ tar zcpfv dokuwiki-backup.tar.gz /path/to/dokuwiki

# unzip
$ tar zxvf dokuwiki-xxxx-xx-xx.tgz


# Example of finding and then tar-ing files
$ find Interfaces/ -name "*DC003*" -mmin -20 -print0 | tar -czvf ~/QF_FBA_Weight/backup.tar.gz --null -T -

# Example of un-taring and creating a target directory for the -C option ($_ is a special bash variable to get the output of the previous command)
$ mkdir -p /target/dir && tar -C $_
```

Julia Evans cartoon of it:
<https://twitter.com/b0rk/status/993682480069824512?lang=en>

![julia evans cartoon of tar](/tar_fromjuliaevans.jpeg){width="800"}

### mkdir creating directories

```bash
# Create a dir, if the parent directories don't exist, create them too
$ mkdir -p /target/dir 

# Can create multiple directories and multiple levels of dirs too
$ mkdir -p /target/{sub1, sub2}/{subsub1, subsub2}
```


### ifconfig is dead, use ip instead

```bash
    # basic command to see addresses in colour
    ip -c a
```

### Disk Usage, Disk Free space

#### NCDU - disk space usage checker

- <https://www.ostechnix.com/check-disk-space-usage-linux-using-ncdu/>

```bash
# install
sudo apt-get install ncdu

# run with
ncdu
```

#### du and df

- Finding usage of current directory + files as a single value

```bash
du -sh .

# to find just in the current directory per folder
du -h --max-depth=1
```

- Finding free space

```bash
df
```

### netstat

```bash
# netstat looking for a particular port number
netstat -laptenu | grep 20005
```

### Lookup hostname from IP address

```bash
# does a lookup on DNS
nslookup <ip address>

# hostname doesn't always work
hostname -a <ip address>
```

### File Permissions

Give user,group and other permissions to read, write and execute

```bash
    chmod ugo+rwx filename

    # simply make a file executable
    chmod +x filename.sh
```

### Find utility

```bash
# find jpg files in the current directory
find . -name '*.jpg'

# find in the current directory files modified in the last minute 
find . -maxdepth 1 -mmin -1

# find with date details and ordering by date 
find . -mmin -15 -printf "%T@ %Tc %p\n" | sort -n

# find .log files and then copy them to ~/someDir
find . -name "*.log" -mmin -45 -exec cp {} ~/someDir \;

# find dirs without a certain filename 
find base_dir -mindepth 2 -maxdepth 2 -type d '!' -exec test -e "{}/cover.jpg" ';' -print

# find and delete - good for deleting lots of files where rm stops working 
find . -name "simulation.log" -delete

# find with multiple matches (from a bash script)
list_of_files="$(find . -type f -name "filename1-*" -or -name "*-filename2")"

# find files where we have .blah and a corresponding .blah.log - finds cases of missing .log files and counts them
find . -name "*.blah" '!' -exec test -e "{}.log" ';' -print | wc -l

# some more examples 
<https://geekflare.com/linux-find-commands/>
```

- find can also be combined with | xargs and in some cases this can be efficient to batch the subsequent commands
  - <https://stackoverflow.com/questions/896808/find-exec-cmd-vs-xargs>
  - With -exec you can end by + instead of \; to batch but may not be the most portable way of writing it.

### List files in directories in a Tree

- <https://www.geeksforgeeks.org/tree-command-unixlinux/>

```bash
# Install if not available on your machine
# List all files and directories including hidden files (-a), to 2 levels with size of each file 
tree -a -L 2 -s

```

### Word Counts - find number of files in dir

- Word Count wc with lots of use cases and examples -
    <https://shapeshed.com/unix-wc/>

```bash
# count the number of files in a dir 
ls -l | wc -l
```

### Grep

Basic command format is:

```bash
grep [options] [pattern] [file]

#If you have the output "Binary file (standard input) matches" whengrep something you know is text,
# you can force grep to treat everything as text using -a
grep -a SomeString log.txt

# other forms of this option: -a, --text, '--binary-files=text'

# example of counting the occurrences
grep -o SOMESTRING myFile.txt | wc -l
```

#### **Other options**

- -i: performs a case-insensitive search.
- -n: displays the lines containing the pattern along with the line
    numbers.
- -v: displays the lines NOT containing the specified pattern.
- -c: displays the count of the matching patterns.
- -r: recursive matches through sub dirs
- -L: display files NOT matching the pattern
- -o: matches only not the full lines
- --include=*.cpp: include files matching the pattern after the = (NB may/may not need the escape wildcard)

### Grep to find text within files

- GNU manual for Grep -
    <https://www.gnu.org/savannah-checkouts/gnu/grep/manual/grep.html#index-_002d_002dno_002dmessages>

```bash
find .  -name "*.edi" -exec  grep  -H -E -o -c  "SomeString"  {} \;
find .  -name "*.edi" -exec  grep  -H -E -o -c  "SomeString"  {} \;
# Find files of a particular name not containing a string - bit at the end is to look for count 0
find .  -name "*.edi" -exec  grep  -H -E -o -c  "SomeString"  {} \; | grep 0

# This is a really nice way to find files of a particular type containing WITHTHISSTRING but not containing NOTTHISSTRING
# The inner grep feeds the filenames of the matches into the outer grep
# -l is to suppress the normal output which includes the matching string
# -L is to find things that DON'T match
grep -rL "NOTTHISSTRING" $(grep -rl WITHTHISSTRING '.' --include=*.cpp)

# Example for finding a lib with a certain symbol 
for lib in `find . -name "*.so"` ; do  grep "someSymbol" $lib >/dev/null; if [ $? -eq 0 ]; then echo $lib; fi  done

# Finding a process with grep and filtering your grep from the result
ps aux | grep some_process | grep -v grep

```

#### Grep patterns

- <https://www.digitalocean.com/community/tutorials/using-grep-regular-expressions-to-search-for-text-patterns-in-linux>

```bash
# Example using grouping with alternative matches
$ grep -E "(GPL|General Public License)" GPL-3

Output:
The *GNU General Public License* is a free, copyleft license for...
Developers that use the GNU *GPL* protect your rights with two steps: ...
  
```

### System Suspend from commandline

- <https://unix.stackexchange.com/questions/484550/pm-suspend-vs-systemctl-suspend>

### Ubuntu on a netbook

<https://wiki.ubuntu.com/HardwareSupport/Machines/Netbooks>

### Docker Installs for Linux - Ubuntu

- <https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce>

- Add the repo for Docker to the Ubuntu install
- Install Docker

- Docker Daemon info - <https://docs.docker.com/config/daemon/>

```bash
#once the repos are setup - install docker-ce
sudo apt-get install docker-ce

# These commands will download the docker images and run a container
sudo docker run hello-world
sudo docker run -it ubuntu bash

```

#### Example of the output from the hello world container

> Hello from Docker!
> This message shows that your installation appears to be working correctly.
>
>To generate this message, Docker took the following steps:
>
> 1. The Docker client contacted the Docker daemon.
> 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
>    (amd64)
> 3. The Docker daemon created a new container from that image which runs the
>    executable that produces the output you are currently reading.
> 4. The Docker daemon streamed that output to the Docker client, which sent it
>    to your terminal.

### Mini Cheatsheet

```bash
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq
```

### Learning Docker

- Overview - <https://docs.docker.com/engine/docker-overview/>
- Getting Started -
    <https://docs.docker.com/get-started/#containers-and-virtual-machines>
- Developing with Docker -
    <https://docs.docker.com/develop/#develop-new-apps-on-docker>
- Java workshop with Docker -
    <https://github.com/docker/labs/tree/master/developer-tools/java/>

### Docker Compose

<https://docs.docker.com/compose/install/>

Docker compose is a tool to scale up docker containers using a yaml file
to describe the deployment.

- <https://nickjanetakis.com/blog/docker-tip-45-docker-compose-stop-vs-down>

```bash
    docker-compose stop # stop container
    docker-compose down -v # stop and remove container
```

### XHCI issues

- <https://bbs.archlinux.org/viewtopic.php?id=236536>
- <https://askubuntu.com/questions/1035528/ubuntu-18-04-systemd-udevd-uses-high-cpu-conflict-with-nvidia-graphics>
- <https://www.maketecheasier.com/4-ways-to-get-yourself-out-of-a-ubuntu-crash/>

### Screenshots

- Simplest is Screenshot application bundled with ubuntu
- Also a list of options -
    <https://www.tecmint.com/take-or-capture-desktop-screenshots-in-ubuntu-linux/>

## List of Linux Topics

- Vim - make a cheatsheet
- User permissions + groups + changing them
- tee command - multiple output destinations
- hard links vs soft links + how files are deleted
- cheatsheet of file structures /bin /dev /etc
- df du -h option
- cheatsheet for find
- more and less cheatsheet
- wc wordcount util
- grep cheatsheet
- cut, split, tail cheatsheet
- using tail for filtering lists even output of file listing with ll
- find some file compare utilities - diff comp comm
- sed awk cheatsheet
  - Need to know the vim commands for this too
- tar gzip option j-\> bzip2

## Vim Cheatsheet

- VIM Cheatsheet - <https://vim.rtorr.com/>

### General text manipulation

```bash
# Cutting, copying and pasting lines
yy # copy
2yy # copy 2 lines
dd # cut

p # paste after
P # paste before

# Finding
/searchstring

```

- Link to VIM searching page - <https://vim.fandom.com/wiki/Searching>

## Less Cheatsheet

- <https://www.thegeekstuff.com/2010/02/unix-less-command-10-tips-for-effective-navigation/>

```bash
# Navigating within less
g - jump to beginning
G - jump to end

/someString - search for "someString" and highlight occurrences n next
occurrence N prev occurrence

```
