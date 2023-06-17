# MKS-CANBUS

Setting Up Klipper ON the MKS-SKIPR Main Controll Board and the THR36/42 Tool Head Board

Download the image file fome here: https://github.com/redrathnure/armbian-mkspi/releases

Install in the SD Card or eMMC via Rufus: https://rufus.ie/en/

Recommend plugging the MKS-SKIPR or MKS-PI directly into ethernet for the primary setup

Insert/connect your flash drive of choice and boot up the control board

If you have a display connected, you can obtain the IP address from there, if not, try an app called "FING" for your smart phone or any other app similar and scan your network to find the IP address asigned to the control-board.

Note, you can just plug in a HDMI screen to the HDMI port, but this must be done before you power up the board, or the display output will not work.

Once you have the IP address, just use command promp and log into your control board using: ssh root@192.168.0.123 (Replace this address with your own)

Default password is: 1234

Now it will ask you to set a password for root, once that is completed it will ask you to create a user account, I will use "nexgen3d", this is the account you and the printer will use, then it will ask you to set a password for that account.

Once that has all complete, type: exit

Then log back into the board using: ssh nexgen3d@192.168.0.123 (Use your user name you set in the previous step, and replace the IP with the IP of your actula board)

Now run: sudo apt update

Once that has completed, run: sudo apt upgrade

Go have a coffee, or a beer, the latter is prefered.

Once that has completed (the update, not the beer), type: sudo reboot

After the reboot has complete, log back into the board using: ssh nexgen3d@192.168.0.123 (Use your user name you set in the previous step, and replace the IP with the IP of your actual board)

Now we are getting to the good part, installing Klipper, make sure you are in your home folder, by typing: cd ~

Then type: cd ~ && git clone https://github.com/th33xitus/kiauh.git

Once completed, then type: ./kiauh/kiauh.sh

You should now see the KIAUH interface, and we will use this to install Klipper and all required componants.

Select Option 1: Install -> We will return to this menu after each module has installed.

Select Option 1: Klipper -> Select Option 1: Python 3.x -> Leave the next option as 1 and hit enter.

Now the base files for Klipper are being install, you should receive a prompt for your password, completed that and press enter.

Coffee time again :) wait for all the packages to install, once completed you will be back into the KIAUH interface.

We are now ready to install the next module, Moonraker, no not he James Bond film, but the Moonraker componant for Klipper.

In the KIAH Interface, Select Option 2: Moonraker -> You will now see a promt to install, please type Y and hit enter, now wait for all the gobbledy-Gook to complete....again.

After all that has completed, you will be back in the KIAUH Interface again, and we are now ready to install the GUI/Interface of your choice, for me, I like Mainsail, but you might not, so install the one of your choice, but for the printers, control boards and upgrade kits I sell, I only support Mainsail, I do this as its easier for me to assist my customers.

Select Option 3: Mainsail -> more of that gobbly-gook, wait, then another prompt to download macros, type Y and press enter, after thats completed, you will be back in the KIAUH interface.

Next we will install Klipperscreen, I support the 3.5" and 5" displays from Makerbase, the controlboard can run other HDMI displays, if you are not planning on running a touchscreen, then you can skip this next module.

Select Option: 5 -> Klipperscreen -> Again, more crazy stuff happening, just wait for all the cool code like stuff to complete, this one can take a while, so more coffee, or maybe beer :)

Now last module to install, only if you plan to use a USB webcam, if you are, please be aware of the very small 5v power budget of the MKS-SKIPR, the USB 5v is shared with SOC and can be limiting, so you may want to invest in a powered USB Hub, try and find one that is powered by a 24v power brick, as this will simplify your wiring, I'm personally not a fan of those little cheap buck conveters, I have had them fail to many times in the past, most printers work onj 24v, so try to use 24v parts.

Select Option 11: Crowsnest -> Again, more hacker like cool movie code like stuff.

You will see a promt asking to add this module to the update module, should already have Y typed on the screen, so just press enter, this just adds Cowsnest to the nice GUI update menu in Mainsail make it a simple procedure to update the software in the future....we hope :)

And lastly, you will see a prompt to rebbot now, change the N to a Y and press enter.

Give it a minute or two to reboot and log back in using SSH again, this image of Armbian is quite fast, and boots very quickly, unlike the version supplied from Makerbase.

Once you back into the system, we will now prepare, creat and download the Klipper firmware files we need to flash to the control boards.

# SECTION: 5 - Klipper Firmware

Type: cd ~

This ensures you are in the home folder, if you type: ls -a

You will see all the things we just installed, most of these are folders, the one we will be jumping into is "klipper"

Type: cd klipper

Type: make menuconfig

Now you will be in the Klipper firmware configuration menu.

You will need to hit the space bar on this one: Enable extra low-level configuration options

You will now see some addition items appear under it, please select: Micro-Controller Architecture -> Then in the next menu, select: STMicroelectronics STM32

Next option, select: Processor model -> Please select: STM32F407

Next option, select: Bootloader offset -> Please select: 48KiB bootloader

Next option, select: Clock Reference -> Please select: 8 MHz crystal

Next option, select: Communication interface -> Please select: Serial (on USART1 PA10/PA9)

Next Option "Buad rate for serial port" leave this at 250000, if its set to something else, then change it to 250000

Ignore the last option about GPIO pins as this is not required.

Now you can press Q and a save prompt will pop up, click Y to save.

Now that we have configured everything, we can now compile the firmware.

Type: make

Look mum, I'm a programming guru :) -> wait for that to complete.

Now, create a folder on your PC, I went with a folder called klipper on my C drive, for simplistic reasons.

Now open a fress command prompt or power shell promt and past the following line into it, but change the username to the one you setup, and change the IP address to your one: scp nexgen3d@192.68.0.123:~/klipper/out/klipper.bin C:\klipper\klipper.bin

If that worked, then you will have the firmware file on your PC, now rename it to: mks_skipr.bin

Copy mks_skipr.bin to an SD-Card that has been formatted in FAT32 then shut down your MKS-SKIPR board and insert the SD-Card into the MCU SD-Card slot, there is two on the board, make sure its the correct one or you may tear a hole in the space time continuum and create some sort of spacial anomoly that will cause a reverse deflagrating implosion.....no not really :)

Power the board up, wait a minute, then powerdown and pull the SD-Card, you have now successfully flashed your MKS-SKIPR board with Klipper.








scp nexgen3d@192.68.0.123:~/klipper/out/klipper.bin C:\klipper\klipper.bin

MCU-TF Slot

Install Input Shaper:
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
~/klippy-env/bin/pip install -v numpy


