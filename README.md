# MKS-SKIPR-SETUP

### This is still a work in progress, and I will update the guide on a regular basis, make corrections as I find them, as well as provide files to support everything.

## Section 1: 

### Install the Operating System on The MKS-SKIPR (Also The MKS-PI)

Setting Up Klipper ON the [MKS-SKIPR](https://nexgen-printing.com.au/online-store/ols/products/makerbase-mks-skipr-3d-printer-control-board-runs-fluidd-os-voron-klipper-onboard) Main Control Board and the `THR36/42` Toolhead Board

**This tutorial was done via Windows (Please Dont Flame Me :), but can be easily addapted to MacOS or your faverite Linux flavour.*

* Download the image file from here: [Armbian-MKSPI](https://github.com/redrathnure/armbian-mkspi/releases)
*I recommend the bullseye current version, through all my testing, this was the fastest to boot and had no issues that I could find, if the something has changed on that repo, I will mirror the version of Armbian that I used link will be added*
* Flash the above image to your the SD Card or eMMC via Rufus: [RUFUS](https://rufus.ie/en/)
* I highly recommend plugging the MKS-SKIPR or MKS-PI directly into ethernet for the primary setup and will save you lots of issues, wifi can later be setup via [Klipperscreen](https://klipperscreen.readthedocs.io/en/latest/) or through `SSH` by running this command:
```console
sudo armbian-config
```
* Insert/connect your flash drive of choice and boot up the control board, note if using and SD Card there is two slots, youy must use the one marked `HOST-TF`
* If you have a display connected, you can obtain the IP address from there, if not, try an app called [FING for Android](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=en_AU&gl=US) or [FING for Apple](https://apps.apple.com/us/app/fing-network-scanner/id430921107) for your smart phone or any other app similar and scan your network to find the IP address asigned to the control-board, will ba called `mks-pi`, or you could also find it via your router/switch.
**Note:** *You can plug in a HDMI screen to the HDMI port, but this must be done before you power up the board, or the display output will not work.*
* Once you have the IP address, just use a command promp in Windows, you dont need putty, the default command promt will work just fine, and log into your control board using the following command, but change the ip address to your specific address: 
```console
ssh root@192.168.0.123
```
* Default password is: `1234`
* Now it will ask you to set a password for root, once that is completed it will ask you to create a user account, I will use `nexgen3d` this is the account you and the printer will use, then it will ask you to set a password for that account as well.
* Once that has all completed, type the following and it will kick you out of SSH: 
```console
exit
```
* Log back into the board using the following, but replace the user name with the one you created in the previous step and your IP address for the board: 
```console
ssh nexgen3d@192.168.0.123
```
* Once your back in, run: 
```console
sudo apt update && sudo apt upgrade
```
* Next step is to go have a coffee, or a beer, the latter is prefered **(as this can take a litle while)*.
* Once that has completed (the update, not the beer), type: 
```console
sudo reboot
```
* After the reboot, log back into the board using the following, but replace the user name with the one you created in the previous step and your IP address for the board: 
```console
ssh nexgen3d@192.168.0.123
```
**Stay logged in and move onto Section 2**

## Section 2: 

### Install Klipper

* Now we are getting to the good part, installing Klipper, make sure you are in your home folder, by typing: 
```console
cd ~
```
* We are now going to install [KIAUH](https://github.com/th33xitus/kiauh), no not the car, the awesome easy to use Klipper automated install tool: 
```console
cd ~ && git clone https://github.com/th33xitus/kiauh.git
```
* Once completed, then type: 
```console
./kiauh/kiauh.sh
```
**You should now see the [KIAUH](https://github.com/th33xitus/kiauh) interface, and we will use this to install Klipper and all required componants.**
* Select Option 1: `Install` **We will return to this menu after each module has installed*
* Select Option 1: `Klipper` Select Option 1: `Python 3.x` Leave the next option as `1` and hit enter.
* Now the base files for Klipper are being installed, you should receive a prompt for your password, completed that and press `Enter`.
* Coffee time again :) wait for all the packages to install, once completed you will be back into the [KIAUH](https://github.com/th33xitus/kiauh) interface.
**We are now ready to install the next module, `Moonraker` no not the cool James Bond film from the 80's, but the Moonraker componants for Klipper**
* In the [KIAUH](https://github.com/th33xitus/kiauh) Interface, Select Option 2: `Moonraker` You will now see a promt to install, please type `Y` and hit `enter`, now wait for all the gobbley-Gook to complete....again.
**After all that has completed, you will be back in the [KIAUH](https://github.com/th33xitus/kiauh) Interface again, and we are now ready to install the GUI/Interface of your choice, for me, I like Mainsail, but you might not, so install the one of your choice, but for the printers, control boards and upgrade kits I sell, I only support Mainsail, I do this as its easier for me to assist my customers if I choose just one.**
* Select Option 3: `Mainsail` More of that gobbley-gook text stuff, wait, then another prompt to download macros, type `Y` and press `Enter`, after thats completed, you will be back in the [KIAUH](https://github.com/th33xitus/kiauh) interface.
* Next we will install [Klipperscreen](https://klipperscreen.readthedocs.io/en/latest/), I support the 3.5" and 5" displays from Makerbase, the controlboard can run other HDMI displays, if you are not planning on running a touchscreen, then you can skip this next module.
* Select Option: 5 -> [Klipperscreen](https://klipperscreen.readthedocs.io/en/latest/) -> Again, more crazy stuff happening, just wait for all the cool code like stuff to complete, this one can take a while, so more coffee, or maybe beer again :)
* lastly, you can safely quit KIAUH and you will be in the terminal, please type:
```console
sudo reboot
```
* Give it a minute or two to reboot and log back in using `SSH` again, this image of Armbian is quite fast, and boots very quickly, unlike the version supplied from Makerbase.

**Once you're back into the system, we will now prepare, create and flash the Klipper firmware filesto the MCU on the control boards** *(This step is not required for the MKS-PI, its only required for the MKS-SKIPR)*.

## SECTION: 3 

### Create and Flash Klipper Firmware For MKS-SKIPR

* Type: 
```console
cd ~
```

* This ensures you are in the home folder, if you type: 
```console
ls -a
```
You will see all the things we just installed, most of these are folders, the one we will be jumping into is `klipper`

* Type: 
```console
cd klipper
```
Then Type: 
```console
make menuconfig
```
**Now you will be in the Klipper firmware configuration menu.**
* You will need to hit the space bar on this one: `Enable extra low-level configuration options`
* You will now see some addition items appear under it, please select: `Micro-Controller Architecture` -> Then in the next menu, select: `STMicroelectronics STM32`
* Next option, select: Processor model -> Please select: `STM32F407`
* Next option, select: Bootloader offset -> Please select: `48KiB bootloader`
* Next option, select: Clock Reference -> Please select: `8 MHz crystal`
* Next option, select: Communication interface -> Please select: `Serial (on USART1 PA10/PA9)`
* Next Option `Buad rate for serial port` leave this at `250000`, if its set to something else, then change it to `250000`
* Ignore the last option about GPIO pins as this is not required.
* Now you can press Q and a save prompt will pop up, click Y to save.
**Now that we have configured everything, we can now compile the firmware.**
* Type: 
```console
make
```
**Look mum, I'm a programming guru :) -> wait for that to complete.**

**Now, create a folder on your PC, I went with a folder called `klipper` on my `C drive`, for simplistic reasons.**
* Now open a fresh command prompt or power shell promt and past the following line into it, but change the username to the one you setup, and change the IP address to your one: 
```console
scp nexgen3d@192.68.0.123:~/klipper/out/klipper.bin C:\klipper\klipper.bin
```
**If that worked, then you will have the firmware file on your PC in the folder you created called `klipper.bim` now rename it to: `mks_skipr.bin`**
* Copy `mks_skipr.bin` to an SD-Card that has been formatted in `FAT32` then shut down your MKS-SKIPR board and insert the SD-Card into the `MCU SD-Card slot`, there is two on the board, make sure its the correct one or you may tear a hole in the space time continuum and create some sort of spacial anomoly that will cause a reverse deflagrating implosion.....no not really :)

**Power the board up, wait a minute or two, then powerdown and pull the SD-Card, you have now successfully flashed your MKS-SKIPR board with Klipper.**

## Section 4: 

### Create and Flash Klipper Firmware for The MKS THR36 and THR42 Tool Head Boards

**Before we start, I state this, and to back it up, a quick article that I wish I found before I wasted many days of my life, DO NOT BOTHER WITH CANBUS, its a total crock of shit, and should stay in cars or whatever else its used for.**

https://os.ratrig.com/blog/no-you-dont-want-to-use-can/

Thank you Mikkel https://github.com/miklschmidt I only wish I had found your article before I flushed days of my time down the toilet hunting and finding bugs and gremmlins with this BS called CAN.

**Now that my rant is out of the way, we can begin, Log back into your board via SSH**
* Type:
```console
cd ~
```
* This ensures you are in the home folder, if you type: 
```console
ls -a
```
**You will see a folder called `klipper` this is where we are headed again.
* Type: 
```console
cd klipper
```
* Type: 
```console
make menuconfig
```
**Now you will be in the Klipper firmware configuration menu.**
* You will need to hit the space bar on this one: `Enable extra low-level configuration options`
* You will now see some additional items appear under it, please select: `Micro-Controller Architecture` Then in the next menu, select: `Raspberry Pi RP2040`
* Next option, select: `Bootloader offset` Please leave it as: `No bootloader`
* Next option, make sure its on: `Flash chip (W25Q080 with CLKDIV 2)` If not change it
* Next option, select: `Communication interface` Please select: `USB`
* Next Option: `USB ids` leave this alone
* Next Option: `GPIO pins` leave this alone
**Now you can press `Q` and a save prompt will pop up, click `Y` to save.**

### Transfer the firmware to your PC
* Now, using the folder we created on our PC in the previous section `c:\klipper`
* Open a fresh command prompt or power shell prompt and paste the following line into it, but change the username to the one you setup, and change the IP address to your own: `scp nexgen3d@192.68.0.123:~/klipper/out/klipper.uf2 C:\klipper\klipper.uf2`

Now you will need to connect the THR board to your PC via a USB cable, set the appropriate jumper to USB Power, then connect to the PC, once connected, press hold down the `Boot` button then press and release the `Reset` button, then you can release the `Boot` button and if all went well, you will have a flash drive show up as `RPI_RP2` just drag and drop the klipper.uf2 firmware file into this flash drive, and in a second it will self flash and reboot itself, all done.

### Note: Make sure you change the USB power jumper back to board power or you run the risk of frying something


[NexGen 3D Printing}(https://nexgen-printing.com.au/) is a Western Australian based 3D Printing company, we specialise in custom 3D printer upgrades and do our best to promote open source software, we believe, if you dont have full root access, then you generally dont own it.

If you like what I have done here and would like to support this kind of work, please feel free to purchase something low cost from my website, like a [Nozzle](https://nexgen-printing.com.au/online-store/ols/products/hardened-steel-nozzles-triple-pack-0-dot-4-0-dot-6-0-dot-8) or one of our inhouse designed and manufactured [MK3 Nano Extruders](https://nexgen-printing.com.au/online-store/ols/products/sherpa-micro-nexgen-nano-extruder)

