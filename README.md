# OS-X-Yosemite-on-Unsupported-Macs
This will include patches/tutorial on how to install OS X Yosemite on Unsupported Macs

Apple History
 
OS X 10.6 Snow Leopard was the first OS X version with optional support for a 64-bit kernel, allowing booting either with a 32-bit or 64-bit kernel. However, Apple did not support booting the 64-bit kernel in Macs that shipped with EFI32 firmware, even if they had 64-bit processors capable of running the 64-bit kernel. When Apple dropped the 32-bit kernel entirely from OS X, starting with OS X 10.8 Mountain Lion, EFI32 Macs no longer had an Apple-supported mechanism to boot newer OS X versions.
 
Fortunately, we have found a work around for these version of OS X. Here we provide guides in Post 1 and 2 and support for Installing OS X Yosemite on your Unsupported Mac.
 
This first post is usually updated with recent summarized information, updates, and more solutions.
 
For those who have 2006/2007 Mac Pros, you may be best suited to using Mr. Zarniwoop's Guide here.
 
Prerequisites
Tested Macs listed below. Here are the minimum requirements:
- Running 10.7 Lion
- At least 2GB of RAM.
- A copy of Yosemite in Applications Folder (.app file preferred)
- 15 GB of free space from USB or HDD Partition.
 
-MacBook2,x
-MacBook3,x
-MacBook4,x
-MacBookPro2,x
-MacBookAir1,1
-MacMini1,x (C2D upgraded)
-MacMini2,x
-iMac4,x (C2D can be upgraded)
-iMac5,x
 
We DON'T assist with Hackintosh. All private messages/emails involving installing OS X on non-Apple hardware will be redirected to another support team.
 
 
Guide to Installing OS X Yosemite on Unsupported Macs
 
ANY HARM OR DAMAGE CAUSED BY THIS GUIDE HAPPENED UNDER YOUR OWN RESPONSIBILITY!
 
Be sure to have root privileges (administrator password) as OS X will prompt you for this on some stage.
 
 
A: PREPARING THE INSTALLATION DRIVE
 
1a: Make a BACKUP of your system if you can.
 
2a: I have some attachments below to help shave off a couple of hours.
 
3a: Get an OS X Yosemite Installer app (Recommended from the Mac App Store)
 
4a: Make sure you have an Intel-Based Mac that supported OS X 10.7 Lion
 
 
B: Get the Flash drive ready
 
1b: Get an empty USB-Stick (8GB or more)/use an external hard disk
 
2b: backup everything on the drive to another drive
 
3b: open Disk Utility and select your drive for installation
 
4b: select the partition tab -> advanced options -> GUID
 
5b: chose a drive name -> select HFS+ as the partition format -> partition the drive
 
 
C: Start the Modifications
 
1c: in Finder right-click the app and select show package contents
 
-> navigate to /Contents/Resources/SharedSupport and double-cick the dmg-file
 
2c: show hidden files in Finder (use included DisAppear.app)
 
3c: in Finder navigate to the Drive you've just mounted
 
4c: locate BaseSystem.dmg -> drop it to the lower Disk Utility side pane
 
5c: select your previously created install partition (not drive!) -> restore tab -> drop the image from the side pane to the source field
 
6c: restore
 
7c: in Finder locate the mounted InstallESD and copy the "Packages" folder
 
8c: past the folder to /System/Installation/ -> you will need to replace the file in there with the actual folder.
 
 
D: Get the Flash drive ready
 
1d: You will have to replace the files without corrupting them. Some of the files are signed so be careful not to change anything else.
 
2d: run the IORegistryExplorer.app -> make sure in the top left corner IOServices is selected
 
3d: under root select your Mac(model) -> on the right at the top copy the board-id value.
 
4d: open /System/Installation/Packages/InstallableMachines.plist -> search for the last entry and replace it
 
5d: open /System/Library/CoreServices/PlatformSupport.plist
 
-> search for the last entry of board-ids and replace it
 
-> search for the last entry of Macs and insert yours as found in the IORegistryExplorer.app
 
6d: OSInstall.mpkg
 
-> make a copy of the /System/Installation/Packages/OSInstall.mpkg into a temporary folder for editing
 
-> Open the OSInstall.mpkg via Flat Package Editor, then drag the 'Distribution' file to a temporary folder
 
-> add the Board-ID to the 'Distribution' file in the line 'var platformSupportValues=[" ... "];' with a simple Plain-Text-Editor in the same manner as the already existing ID's and save it.
 
-> Delete the old Distribution file in the Flat Package Editor and add in the new one.
 
-> replace the original OSInstall.mpkg in the Installer with the edited one.
 
7d: BaseSystem
 
-> copy BaseSystem.dmg and BaseSystem.chunklist into the root folder of the USB-Flashdrive or HDD
 
8d: Kernel
 
-> extract the Kernel using the Pacifist.app from the original InstallESD.dmg > Packages > Essentials.pkg > /System/Library/Kernels/kernel
 
-> create a folder named "Kernels" in System/Library/
 
-> add the extracted kernel file to /System/Library/Kernels/
 
8d (Optional): Boot.efi
 
-> If your older Mac has a 32bit EFI (EFI32) replace the Boot.efi in /System/Library/CoreServices/ as well as /usr/standalone/i386 with the version we provided or in Post 2.
 
 
E: Installation
 
1e: reboot your Mac holding option (cmd) key
 
2e: select the USB drive (BaseSystem) and press enter
 
3e: when booted click install/continue until you reach the disk selection menu
 
-> select you main drive (probably Macintosh HD) if you are sure about it, else select another empty drive (at least 15GB for testing/bigger if it should be a secondary system)
 
4e: finish installation
 
(If the Mac does not reboot to the Yosemite desktop boot to the install-drive again and perform the following.
 
Boot back into the Yosemite Install Partition
 
open the terminal at the top menu bar or boot into single user mode (Hold Command -S immediately afterturning on)
 
enter: sudo rm /Volumes/[Main Drive Name]/System/Library/CoreServices/PlatformSupport.plist
 
 
F: Install these 64 bit Kexts from OS X Hackers link below (These will better the graphics by a little but you will not have Graphics Acceleration. Still in beta so they may not work well)
 
1f: open the KextUtility.app by dropping all of the files inside this attachment zip folder named “kexts. . ." to it. Don't forget to drop in the AppleHDA.kext
 
2f: reboot
 
3f: Boot into Single User Mode (Hold Command-S after hearing the bong sound)
 
4f:enter: sudo nvram boot-args="kext-dev-mode=1"
 
5f: reboot again normally
 
 
IF your Macbook can't wake up from sleep:
 
Because of lack of working Graphics Acceleration. Your Macbook may not be able to wake from a display sleep
 
Install the NoSleep Extension
Set the Preferences to Never Sleep on AC Adapter and Battery
Check the 'Start NoSleep Utility on system startup' setting
Your Macbook screen will never turn off unless your actually shut down your Macbook.
 
CONGRATULATIONS!!!
 
Bugs (from multiple Mac Models)
 
 
1. Maps does not view the maps
 
2. Launchpad is somewhat delayed and choppy
 
3. Video don’t play in iTunes, Safari, nor DVD Player (best use Quicktime and Google Chrome)
 
4. Notification Center is sometimes a mess.
 
5. Only one Screen Resolution available
 
6. Some Apps will have artifacts if primary using Graphics Card.
 
7. iMessage/FaceTime note:
Most users cannot initially login to iMessage or FaceTime using their Apple ID from their Macs after installing Yosemite as a security precaution. When trying to login, they receive an iMessage Registration validation code. The solution is to contact Apple support, provide the Mac's serial number, explain that Yosemite was installed using our guide and that iMessage isn't working and provide the validation code. Apple then unblocks the Mac, allowing iMessage and FaceTime login immediately and in the future OS updates.
 
OS X Software Updates
 
Updating . . .
 
Airdrop
 
Updating. . .
 
Support
 
Feel free to post your questions, concerns, or success story. If you can’t post us back because your only usable device is bricked, Skype me at TMRJIJ or email us at support@osxhackers.honor.es . we'll try to respond within 1-2 days.
 
Be sure to thank our awesome developers who have contributed greatly.
 
Downloads/Files for Patching
 
Files Needed for OS X Yosemite Patch only are on OS X Hackers:
Download: http://sh.st/piGuc
 
 
The OS X Hackers App for Mac (10.7 or later) with all Patch files for Mavericks and Yosemite [Updated January 21, 2015]:
Download: http://sh.st/pzb9M
 
 
The Steps above can also be done by Oemden's SFOTT script:
SFOTT app script: http://oemden.com/?page_id=531
 
MacPostFactor v0.2b1 has been released by Wayne Wong (@Wayne_819) and Kelian Dumerais (@MLforAll):
Go to Post: http://forums.macrumors.com/showpost.php?p=20525246&postcount=4093
 
We are working on the Guide to 'Windows 8 BootCamp on Unsupported Macs.' Here is our first method guide:
BootCamp Guide (Closed Beta): http://sh.st/pDWPE
 
OS X Hackers are is not affiliated with Apple Inc. Mac OS Ten (X), Mac, iOS, iPhone, iPad, and all other Apple product names are trademarks or registered trademarks of Apple Inc. All other company and product names are trademarks or registered trademarks of their respective companies.
 
MacPostFactor was made by Wayne Wong (@Wayne_819) and Kelian Dumarais (@MLforAll)
 
Guide and OSXH site/app designed by Isiah Johnson (@TMRJIJ) and Robby Sharpero and is provided by Johnson Network.
 
Developers:
 
Liem Mai, Birtha Åbel, Wayne Wong, Kelian Dumarais, Nolen Johnson, Mr. Zarniwoop, Atvusr, Tiamo, oem
