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






scp nexgen3d@192.68.0.123:~/klipper/out/klipper.bin C:\klipper\klipper.bin

MCU-TF Slot

Install Input Shaper:
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
~/klippy-env/bin/pip install -v numpy


