# Installing MetaRepo, and how it works
*This guide will explain how to install MetaRepo on the NAS326, and explains how it works*

---
So to begin, you'll need to prepare the NAS326. You will probably want to go into Control Panel and choose TCP/IP under Network, then assign your NAS326 a static IP address on your local network using the Network Interface tab.

You'll then want to go to Network and then Terminal, then choose to turn SSH on, but leave Telnet off for security.

You'll also want to ensure you have a RAID volume initialised and working, as you'll be using the NAS326's hard drives to install everyting (the onboard flash is *kinda* read-only, its an oddball, I've not yet worked out how it works, only that the Arch Linux OS gets loaded into RAM from it to run).

---
## What is it?
MetaRepository is a small CGI script which attaches itself to the normal ZyXEL web UI. It will take over the App Center, changing where it downloads it's app lists from. It will also allow you to add your own custom app list locations should you desire. When installing MetaRepository, it will initially take over all of the app list and therefore will prevent other apps from appearing in the App Center available app list. Once installed, all of the ZyXEL official packages will become available to download again, in addition to a bunch of third-party apps which are now available. These third-party apps are what MetaRepository adds, and you can use MetaRepository to add your own apps using your own repository as mentioned above. To add your own app repositories using MetaRepository, there is a new app icon on the ZyXEL web UI desktop, which will take you to the MetaRepository configuration page which has it's own examples of how to use it.

![MetaRepository Configuration](./img/metarepoconf.png?raw=true)

---
## Installation
 - To begin, make sure you are logged in as the admin user to the ZyXEL web UI and also logged in as root to the SSH terminal (root and admin have the same password, even if you change admin's password).
 1. (On SSH) Run `cd /i-data/sysvol/admin` to navigate to your RAID volume's `admin` folder. Create the required directory by running `mkdir zy-pkgs` and enter it by running `cd zy-pkgs` . This is where the config file we are about to create is read from automatically.
 2. Run `vi web_prefix` . In the newly opened editor, Press `i`, paste the following url `http://downloads.zyxel.nas-central.org/Users/Mijzelf/zypkg-repo/` exactly as shown and then press `ESC`, `:`, `w`, `:`, `q` then finally `ENTER`. This simply opens the file in Vim (no nano available YET, later though), switches to insert mode, inserts the URL, exits insert mode, saves and then exits.
 3. (On ZyXEL web UI) Open the App Center, go to Browse then All Apps. Press the refresh button in the top left.
 4. MetaRepository should be the only item to appear. Hit `install` and let it complete. Then press the refresh button in the top left again. All of the ZyXEL official packages should reappear, in addition to the third-party packages provided by MetaRepository by default.

 ![Installing MetaRepository](./img/metarepoinst.png?raw=true)

 ---
 ## Known issues
 If refreshing after installing MetaRepository fails or nothing other than MetaRepository appears, first disable MetaRepository, refresh, enable and then refresh.

 If the issue still persists, ensure the DNS setting on the NAS are correct.