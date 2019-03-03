# ZyXEL NAS326 Hacking and Modernisation
**Disclaimer**: I am not responsible for any use or interaction with this guide. This guide is provided to be educational and additionally provide a useful end result which is a NAS326 by ZyXEL becoming more capable than ZyXEL currently supports it for.

---
## How this all started
So I recently purchased a NAS326 from Amazon for around £100. This is a 2 bay NAS which appears to run an extremely cut down version of Arch Linux ARM, with an unlocked UBoot boot loader. The device seems very capable in itself, with an App Center for installation of new software provided officially by ZyXEL, however this software appears to be largely outdated. This is where I intend to focus - on the installation of modern software.

**Noob Alert**: I am a noob. Although A lot of what I do will be correct and work fine, it may not be the best and most efficient way. If you want to correct me or provide a better way of doing something, please kindly open an issue. I have absolutely no problem with constructive criticism!

---
## Sources of Information
So I have had many sources of information during the process of working on this NAS. I will provide links (and sometimes direct page links) to as many sources of information as I can think of below:

 - http://nas-central.org/ - Provided most information on existing hacks and NAS details
   - http://zyxel.nas-central.org/wiki/Category:NAS326 - Technical details of the NAS326 including the UBoot map
   - http://zyxel.nas-central.org/wiki/3rd_party_zypkgs - Installation guide used to build my guides for the installation of third party packages on to the NAS326
   - http://zyxel.nas-central.org/wiki/FFP_as_zypkg - FFP which we will use for the installation of packages
 - http://www.craigamos.rocks/building-the-zyxel-nas326/ - Directory structure and Apache config location
 - https://www.smallnetbuilder.com/nas/nas-reviews/33001-zyxel-nas326-2-bay-personal-cloud-storage-reviewed?limitstart=0 - Internal board picture, technical specs
 - https://www.sammyk.me/compiling-php-from-source-writing-tests-for-php-source - PHP compilation from source guide

---
## Goals
All of the guides assume you arte using ZyXEL's 5.21 firmware. In this firmware as few things are broken but the guides whould explain how to fix them.

Here are the goals I intend to achieve. I will mark them as completed as I make my way through them:

 - PHP7
   - Compile and run successfully - DONE
   - Persist across reboots - DONE (ffp install directory)
   - Get working with Apache
 - MySQL Latest
   - Compile and run successfully
   - Persist across reboots
   - Auto start on boot
 - Get a VirtualHost system working on Apache
   - Support HTTP Port 80
   - Support HTTPS Port 443
   - Support multiple subdomains
   - Support other ports
 - Get the latest OwnCloud working

---
## If all the external sources disappear
I intend to keep a copy of all of the resources required to carry out the goals. I will write all of my guided information as if the original resources *DO* exist, and if they suddenly disappear you can either try to grab them on https://archive.org and please open an issue on this repository so I can rewrite parts of the guide so that they work with sources I can provide.

For web resources such as documentation and guides that already exist and I link to, I will try to make sure they are available on https://archive.org by manually starting a page crawl and save.

---
## Guides (ordered)
 - metarepo.md - MetaRepository, the App Center third-party repository tweak
 - ffp.md - FFP, the third-party software manager and insaller
 - php7.md - PHP7, the latest PHP as of writing used for modern web apps on the NAS' Apache server

---
## Contact me!
If there is an issue with this repository in ANY way, such as a broken link, broken instruction in the guide, missing resource or ANYTHING else, please open an issue on the repository.

If you are interested in helping, please contact me via email at ahorner@programmer.net preferrably with some information on what you are capable of doing and i'll see what I can give you as something I cannot do. Of course I will give credit where credit is due!