OS X Yosemite on Unsupported Macs
OS X Hackers

OS X Extracter and MacPostFactor are apps that guide you through patching and installing OS X El Capitan (10.11), Yosemite (10.10), Mavericks(10.9), or Mountain Lion (10.8) on your older Mac. This thread focuses on OS X Yosemite.

MacPostFactor works for Mountain Lion, Mavericks, and Yosemite (certain Models).
Please note that older GPU (GMA 950, X3100, X1600, X1300, X1900, 7300gt, etc.) Graphics Acceleration on Mavericks and Yosemite is not supported yet but this thread consists of many graphical workarounds.
Installing on these models may cause them to have graphical issues as stated in these pages. Kexts are provided to help a little bit.
OS X Extractor is somewhat for more advanced users and should only be used as an alternative to MacPostFactor. This thread consists of members prominent in these patches that can help you solve your issues. Please do not hesitate to post if you have questions.
[​IMG]​

Apple History

OS X 10.6 Snow Leopard was the first OS X version with optional support for a 64-bit kernel, allowing booting either with a 32-bit or 64-bit kernel. However, Apple did not support booting the 64-bit kernel in Macs that shipped with EFI32 firmware, even if they had 64-bit processors capable of running the 64-bit kernel. When Apple dropped the 32-bit kernel entirely from OS X, starting with OS X 10.8 Mountain Lion, EFI32 Macs no longer had an Apple-supported mechanism to boot newer OS X versions.

Fortunately, we have found a work around for these version of OS X. Here we provide guides in Post 1 and 2 and support for Installing OS X Yosemite on your Unsupported Mac.

This first post is usually updated with recent summarized information, updates, and more solutions.

For those who have 2006/2007 Mac Pros, you may be best suited to using Mr. Zarniwoop's Thread here. The MCPF and OSXE projects are not affiliated with them. We will not contact them either. Confrontation has occurred both publicly and privately in MacRumors, the site, and other forms of communications and we don't want anything to do with them and their Mac Models. It simple don't ask Mac Pro questions to people who don't have Mac Pros :p. Your post will be requested to be moved to their thread.
Mac Pro (1,1/2,1) Yosemite Guide: Hennesie2000's Guide here.

Prerequisites
Tested Macs listed below. Here are the minimum requirements:
- Running 10.7 Lion
- At least 2GB of RAM.
- A copy of Yosemite in Applications Folder (Recommended from the Mac App Store)
- 15 GB of free space from USB or HDD Partition to serve as your Installation Drive.

-MacBook2,x
-MacBook3,x
-MacBook4,x
-MacBookPro2,x
-MacBookAir1,1
-MacMini1,x (C2D upgraded)
-MacMini2,x
-iMac4,x (C2D can be upgraded)
-iMac5,x (post #846 might help)

We DON'T assist with Hackintosh. All private messages/emails involving installing OS X on non-Apple hardware will be redirected to another support team.


Guide to Installing OS X Yosemite on Unsupported Macs 

Method 1 - OS X Extractor​

ANY HARM OR DAMAGE CAUSED BY THIS GUIDE HAPPENED UNDER YOUR OWN RESPONSIBILITY!
IF YOU HAVE ANY REGRETS ABOUT DOING THIS TO YOUR MAC, YOU PROBABLY SHOULDN'T DO IT. IF YOU ARE QUESTIONING WHETHER IT IS WORTH IT, YOU SHOULD DEFINITELY NOT TRY THIS.
PLEASE READ THIS GUIDE BEFORE ASKING QUESTIONS? WE HAVE TOO MANY EMAILS AND SKYPE MESSAGES TO ANSWER AND CAN'T BABY YOU THROUGH THIS ONE STEP AT A TIME. IF YOU CAN'T FIGURE YOUR WAY AROUND OS X, YOU SHOULDN'T BE DOING THIS.

Be sure to have root privileges (administrator password) as OS X will prompt you for this on some stage.


A: Preparing The Installation Drive

Make a BACKUP of your system if you can.
OS X Extractor has generally everything you need to patch OS X (There are also numerous other sources that can help).
Get an OS X Yosemite Installer app (Recommended from the Mac App Store)
Make sure your Mac meets the Requirements above

B: Start Patching
Install OS X Extractor.
After you install, there should be a Hidden Toggle in your System Preferences
Right click on the OS X Yosemite Installer app and click show package contents.
Browse to the folder /Contents/SharedSupport
Double-click to mount "InstallESD.dmg"
Open up Disk Utility in Applications/Utilities and drag BaseSystem.dmg to the lower Disk Utility side pane.
Click on BaseSystem.dmg in Disk Utility and select the Restore tab.
Set the BaseSystem.dmg as the source and choose the installation drive (formatted as HFS+ and GUID) as the destination.
Use Finder to browse the newly restored installation drive installer.
Go to the folder /System/Installation on the installation drive and delete the "Packages" alias file. It will be replaced with the actual folder.
Go back to the mounted InstallESD.dmg and drag the "Packages" folder into the /System/Installation folder where the alias file used to be.
Copy the files, ”BaseSystem.dmg" and “BaseSystem.chunklist," to the root of the thumb drive.
Unmount InstallESD.dmg You don't need it anymore.
(for non 64 bit Macs) Unlock and Replace the boot.efi files located in /System/Library/CoreServices and /usr/standalone/i386 with the copy provided in /Applications/OS X Hackers Patch Files/Boot EFI/ or from here . To Unlock it, use the Terminal app in Applications/Utilities/ and enter the command:    
Code:
sudo chflags nouchg /Volumes/OS\ X\ Base\ System/System/Library/CoreServices/boot.efi 
(If you receive an error, go the that directory and find the boot.efi. Then in the Terminal, enter 'sudo chflags nouchg ' and drag the old boot.efi in the window. Press Enter)
Now lock the new boot.efi file
(for non 64 bit Macs) lock the new boot.efi with this command:  
Code:
sudo chflags uchg /Volumes/OS\ X\ Base\ System/System/Library/CoreServices/boot.efi  
Copy the folder named "Kernels", (rename it so if it says "Kernel") from ‘/Applications/OS X Hackers Patch Files/‘ to the ‘/System/Library/Kernels/‘ folder on the installer drive.
replace the original OSInstall.mpkg in the Installation drive (/System/Installation/Packages/) with the modified one from /Applications/OS X Hackers Patch Files/
Next you will have to add your Mac Model to the installer. You will have to replace the files without corrupting them. Some of the files are signed so be careful not to change anything else. Make sure your changes mimics the same syntax as other entries. You may have to copy and paste the quote marks from an existing entry. If your closing quote after the boardID looks italic, you're WRONG!
run the IORegistryExplorer.app from the OS X Hackers Patch Files folder make sure in the top left corner IOServices is selected
under root select your Mac(model) -> on the right at the top copy the board-id value.
open in your Installation Drive, /System/Installation/Packages/InstallableMachines.plist with TextEdit and search for the last entry and replace it with your board-id value
open /System/Library/CoreServices/PlatformSupport.plist and do the same.
Great! The hard part is over. Now it's time for installation. Re-hide the hidden files with the DisAppear.app, Close the Terminal, and Close all other Applications. Take a breather and move on to the next part of the guide.

C: Installation

reboot your Mac holding option (alt) key.
If the installation drive boot you back to the main partition, try blessing the drive from your terminal app:
Code:
sudo bless --folder /Volumes/OS\ X\ Base\ System --file /Volumes/OS\ X\ Base\ System/System/Library/CoreServices/boot.efi --setBoot
select the Installation drive "OS X Base System" (and press enter)
when booted click install/continue until you reach the disk selection menu, select you main drive (probably Macintosh HD) if you are sure about it, else select another empty drive (at least 15GB for testing/bigger if it should be a secondary system)

D: If Reboot Fails

(If the Mac does not reboot to the Yosemite desktop boot to the install-drive again and perform the following.
Boot back into the Yosemite Install Partition
open the terminal at the top menu bar or boot into single user mode (Hold Command -S immediately afterturning on)
enter:
Code:
sudo rm /Volumes/[Main Drive Name]/System/Library/CoreServices/PlatformSupport.plist

E: Install these 64 bit Kexts from the Kexts folder from OS X Extractor 
(These will better the graphics by a little but you will not have Graphics Acceleration. Still in beta so they may not work well)
open the KextUtility.app by dropping all of the files inside this attachment zip folder named “kexts[yourgraphicsmodel…]“ to it. Don't forget to drop in the AppleHDA.kext for sound.
reboot.
Boot into Single User Mode (Hold Command-S after hearing the bong sound)
enter: 
Code:
sudo nvram boot-args="kext-dev-mode=1"
reboot again normally.

IF your Macbook can't wake up from sleep:

Because of lack of working Graphics Acceleration. Your Macbook may not be able to wake from a display sleep

Install the NoSleep Extension
Set the Preferences to Never Sleep on AC Adapter and Battery
Check the 'Start NoSleep Utility on system startup' setting
Your Macbook screen will never turn off unless your actually shut down your Macbook.

CONGRATULATIONS!!!

Method 2 - MacPostFactor

Screen Shot 2015-06-25 at 12.37.39 PM.png
​
IMPORTANT NOTES

Install MacPostFactor at your own risk. We are not liable if your computer explode, fail to wake you up for work, lose important files, pictures, porn or simply ceased to work. Always backup your existing installation before installing MacPostFactor or install in a second partition.

We are not aware of remaining bugs...

Although its been thoroughly tested by us and our group of private beta testers, you might still find bugs in it, and if you do find one, feel free to contact us on Twitter @MLforAll & @IsiahJohnson15 or simply email me at voolfy@me.com (@MLforAll's mail) or support.osxhackers.tk.

Yosemite Install is EXPERIMENTAL. Try this on a secondary partition.

Supplementary Informations for Yosemite

Yosemite can be installed on all computer but ONLY Mac Pros WITH AN UPGRADED GRAPHICS CARD can use graphics acceleration as of now !

Requirements for MacPostFactor to work
◆ A Mac with Core 2 Duo or Xeon Processor.
◆ OS X 10.7 or later
◆ 2GB RAM at least
◆ At least 15GB of HDD space (8GB for USB)
◆ Install OS X Yosemite.app 10.10.0 or later in your Application Folder
◆ Read our instructions on MacRumors at least twice

Friendly reminder.
We're not responsible if you screw up your system. Technically, that won't happen as you can always go back to Lion, Mountain Lion or Mavericks

Instructions — Installing directly on this computer
1 Make sure you have Install OS X Yosemite.app in your Application Folder
2 Select "On this computer" on the main MCPF window. Then, choose the partition you want to install Yosemite on.
3 Click install and prompt your password.
4 Click reboot. Your computer should reboot with the OSXHackers logo.
5 Once booted, Click Continue, Agree and choose the only partition showed.
6 Click reboot when you see "Installation succeeded !".
7 Enjoy!

Instructions — Installing via USB
1 Make sure you have Install OS X Yosemite.app in your Application Folder
2 Select "On an external drive" on the main MCPF window. Then, choose the disk you want to install the Yosemite installer on.
3 Click install and prompt your password.
4 Click exit. Boot the computer you want to install Yosemite on with 'alt' held and select your USB drive.
5 Once booted, Click Continue, Agree and choose the partition you want to install on.
6 Click reboot when you see "Installation succeeded !".
7 Enjoy!



Bugs (from multiple Mac Models)
Maps does not view the maps
Launchpad is somewhat delayed and choppy
Video don’t play in iTunes, Safari, nor DVD Player (best use Quicktime and Google Chrome)
Notification Center is sometimes a mess.
Only one Screen Resolution available
Some Apps will have artifacts if primary using Graphics Card.
iMessage/FaceTime note: Most users cannot initially login to iMessage or FaceTime using their Apple ID from their Macs after installing Yosemite as a security precaution. When trying to login, they receive an iMessage Registration validation code. The solution is to contact Apple support, provide the Mac's serial number, explain that Yosemite was installed using our guide and that iMessage isn't working and provide the validation code. Apple then unblocks the Mac, allowing iMessage and FaceTime login immediately and in the future OS updates. They really don't care.
OS X Recovery Patch

Go to Applications/OS X Hackers Patch Files/Recovery Patcher/
Install the 'Recovery Patcher' pkg (Not working for El Capitan)

OS X Software Updates

Go to Applications/OS X Hackers Patch Files/Software Update Patch/
Install the 'Software Update Patch' pkg
(EFI32 Mac only) Using Pike's Boot.efi, Install the EFI Daemon patch.

Animation Disabler

You don't have Graphics Acceleration, right? Then you don't need excess Animation slowing down your system.
Go to Applications/OS X Hackers Patch Files/Animation Disabler/
Install the 'Disable Graphical Animations' pkg

Airdrop

Go to Applications/OS X Hackers Patch Files/AirDrop Enabler/
Install the 'Enable Airdrop' pkg
Restart

You can send file with AirDrop to other Macs only. Sometimes newer Macs can't find your model.

Support

Feel free to post your questions, concerns, or success stories in this thread. If you can’t post us back because your only usable device is bricked, Skype at TMRJIJ, MLforAll, or email us at Support@OSXHackers.net. We'll try to respond within 3-4 days.
There should be some great support Applications that we will use to help you.

Be sure to thank our awesome developers who have contributed greatly.
 
Downloads/Files for Patching

Files Needed for OS X Yosemite Patch only:
Updating . . .

The OS X Extractor v1.3 with all Patch files for Mountain Lion, Mavericks, Yosemite, and El Capitan [October 2, 2015]:
Download Link: http://osxhackers.net/OSXE




OS X Hackers are is not affiliated with Apple Inc. Mac OS Ten (X), Mac, iOS, iPhone, iPad, and all other Apple product names are trademarks or registered trademarks of Apple Inc. All other company and product names are trademarks or registered trademarks of their respective companies.

MacPostFactor was made by Wayne Wong (@Wayne_819) and Kelian Dumarais (@MLforAll)

Guide and OSXH site/app designed by Isiah Johnson (@TMRJIJ) and Robby Sharpero and is provided by Johnson Network.

Developers/Contributors:

Liem Mai, Birtha Åbel, Wayne Wong, Kelian Dumarais, Nolen Johnson, Mr. Zarniwoop, Tiamo, Pike R. Alpha, oem, atvusr, Jesse Samluk, Mike Hennessie, Andy Vandijck, 666sheep
