# Mac Stuff

- [Mac Stuff](#mac-stuff)
  - [Replacing a failed Hard drive on a Mac](#replacing-a-failed-hard-drive-on-a-mac)
  - [Restoring MacOSx](#restoring-macosx)
    - [Mavericks Migration notes](#mavericks-migration-notes)
    - [Memory Upgrades](#memory-upgrades)
  - [Dual boot linux with mac](#dual-boot-linux-with-mac)
    - [link dump](#link-dump)
  - [MacPorts](#macports)
    - [Cheatsheet](#cheatsheet)
  - [Useful Apps](#useful-apps)
  - [Key Shortcuts](#key-shortcuts)
    - [Screenshots](#screenshots)
    - [Launch an App from the Terminal](#launch-an-app-from-the-terminal)
    - [Opening Multiple Windows for Eclipse](#opening-multiple-windows-for-eclipse)
    - [Modifying file info for multiple files](#modifying-file-info-for-multiple-files)

## Replacing a failed Hard drive on a Mac

- Replace with SSD
- Issues with display connector
- Torx need the tiny one
- Fan issue - SSD Fan Control + Link needed

## Restoring MacOSx

- Install with disk
- problems with fans and sleep times
- getting to right version
- restore from Time machine pretty difficult
- using el capitain from snow leopard but needed first to update to
    10.6.8 before seeing App Store then needed N's ID to connect
    <https://discussions.apple.com/thread/7678883?start=0&tstart=0>
    <https://support.apple.com/en-us/HT206886>
    <https://www.cnet.com/news/how-to-reinstall-the-mac-app-store-in-snow-leopard/>
- Using migration assistant
- Apple ID blocked

- <http://9to5mac.com/2015/02/13/how-to-swap-imac-hard-drive-for-ssd/>
- <https://www.ifixit.com/Guide/iMac+Intel+21.5-Inch+EMC+2389+Hard+Drive+Replacement/6284>
- <https://www.ifixit.com/Guide/iMac+Intel+27-Inch+EMC+2309+and+2374+Hard+Drive+Replacement/1634>
- <http://www.instructables.com/id/Changing-an-iMacs-HDD/step10/Using-your-new-HDD/>
- Using puppy/linux to boot -
    <https://studyblast.wordpress.com/2011/08/14/guide-mac-os-x-lion-how-to-boot-a-linux-live-system-from-a-usb-drive-how-to-update-any-ocz-ssds-firmware/>

### Mavericks Migration notes

- Garmin Issues - looks to be a retransfer of all Activities
- Java issues - needed to install java to begin with + eclipse 3.6 never worked until the Apple java 1.6 update version was installed (seems to have a different structure to oracle java 1.7).
  - All newer versions of eclipse, netbeans etc worked with newer oracle version.
  - Some games seem not to work - eg wolfenstein enemy territory
  - IPCam stuff also seems dodgy - FF and Chrome not working

### Memory Upgrades

- 1333MHz DDR3 PC3-10600 SDRAM

## Dual boot linux with mac

I've used the liveUSB for ubuntu 20 on the iMac and it seems like nearly everything worked - magic mouse + keyboard etc.
I'd like a more permanent setup than the liveusb so maybe linux mint might be cool too.

- Instructions for dual boot install on MacBook Pro - <https://forums.linuxmint.com/viewtopic.php?t=261805>
- DUal boot on imac <https://forums.linuxmint.com/viewtopic.php?t=261805>
- Install on iMac <https://forums.linuxmint.com/viewtopic.php?t=273073>
- Nice step by step guide with pictures - <https://linuxnewbieguide.org/how-to-install-linux-on-a-macintosh-computer/>

### link dump

- From the mint site <https://linuxmint-installation-guide.readthedocs.io/en/latest/partitioning.html>
- <https://apple.stackexchange.com/questions/85121/resetting-mbr-on-imac>
- <https://askubuntu.com/questions/765254/add-grub-menu-for-os-x>
- <https://www.lifewire.com/dual-boot-linux-and-mac-os-4125733#using-refind-as-your-dual-boot-manager>
- <https://forums.bunsenlabs.org/viewtopic.php?id=5136>
- Problem after dual boot install <https://forums.linuxmint.com/viewtopic.php?t=269661>
- talks about install and using refind <https://medium.com/@genebean/dual-booting-macos-high-sierra-and-linux-mint-4bbc21b830ef>
- Again an install but with some links to fixing the boot <https://forums.linuxmint.com/viewtopic.php?t=239565>
  - <https://www.everydaylinuxuser.com/2014/07/how-to-install-linux-mint-alongside-osx.html>
  - <http://askubuntu.com/questions/765254/add-grub-menu-for-os-x>
  - <https://askubuntu.com/questions/1220175/how-do-i-get-the-grub-menu-to-show-on-a-macbook/1299955#1299955>
- Another dual boot install <https://forums.linuxmint.com/viewtopic.php?t=269661>
- Error I get for grub MokListRT <https://askubuntu.com/questions/1279602/ubuntu-20-04-failed-to-set-moklistrt-invalid-parameter>
  - And another on the same error <https://forums.linuxmint.com/viewtopic.php?t=337744>
  - <https://apple.stackexchange.com/questions/85121/resetting-mbr-on-imac>

## MacPorts

Package installer for Mac
Mac ports allows you to install things conveniently from the terminal
window

the command is sudo port ... for most things you want to do.

For migration to OSX Mavericks I followed this migration guide.

<https://trac.macports.org/wiki/Migration>

There's also the guide to macports here: <http://guide.macports.org/>

### Cheatsheet

- sudo port installed
- sudo port selfupdate
- port version
- port list (but this gives a very long list)
- port search <pip> (more precise search)
- port installed (list of installed ports)
- port outdated
- sudo port upgrade outdated
- sudo port select pip (show installed versions)
- sudo port select --set pip pip27

## Useful Apps

- Development apps - <http://www.rockettheme.com/blog/75-mac/499-essential-apps-for-mac-based-development>
- Burning and ripping discs - <http://handbrake.fr/>

## Key Shortcuts

- Pipe in terminal - Alt + Shift + L
- F11 - show desktop
- Tilda ~ - Alt+n

### Screenshots

<http://guides.macrumors.com/Taking_Screenshots_in_Mac_OS_X>

- Command-Shift-3: Take a screenshot of the screen, and save it as a file on the desktop
- Command-Shift-4, then select an area: Take a screenshot of an area and save it as a file on the desktop
- Command-Shift-4, then space, then click a window: Take a screenshot of a window and save it as a file on the desktop
- Command-Control-Shift-3: Take a screenshot of the screen, and save it to the clipboard
- Command-Control-Shift-4, then select an area: Take a screenshot of an area and save it to the clipboard
- Command-Control-Shift-4, then space, then click a window: Take a screenshot of a window and save it to the clipboard

- Can also use also Grab App in Applications/Utilities

### Launch an App from the Terminal

'''bash
 open /path/to/some.app
'''

### Opening Multiple Windows for Eclipse

'''bash
      cd /Applications/eclipse/
      open -n Eclipse.app''
'''

### Modifying file info for multiple files

- Select multiple files, right-click to show options menu.
- Hold down **alt** key and an option **Show Inspector** will appear.
- This will open just one info window instead of one per file

<http://forums.macrumors.com/showthread.php?t=366864>

**Note:** This could also be achieved with a recursive command line
command - chflags -R nouchg ./

<http://www.westwind.com/reference/os-x/commandline/files-folders.html>
