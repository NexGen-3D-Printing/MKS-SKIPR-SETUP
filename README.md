# MKS-CANBUS
Setting Up CANBUS ON the SKIPR and THR

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

Once that has completed, type: sudo reboot

After the reboot has complete, log back into the board using: ssh nexgen3d@192.168.0.123 (Use your user name you set in the previous step, and replace the IP with the IP of your actula board)

Turn on the internal PINs for ADXL345: https://www.klipper3d.org/RPi_microcontroller.html?h=gpio
Turn on the PINS via armbian-config > System > Hardware - toggle on the option there, confim and reboot
Install Klipper via: https://github.com/th33xitus/kiauh
