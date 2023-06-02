# MKS-CANBUS
Setting Up CANBUS ON the SKIPR and THR

Download the image file fome here: https://github.com/redrathnure/armbian-mkspi/releases

Install in the SD Card or eMMC via Rufus: https://rufus.ie/en/

Recommend plugging the MKS-SKIPR or MKS-PI directly into ethernet for the primary setup

Insert/connect your flash drive of choice and boot up the control board

If you have a display connected, you can obtain the IP address from there, if not, try an app called "FING" for your smart phone or any other app similar and scan your network to find the IP address of the control board.

Note, you can just plug in a HDMI screen to the HDMI port, but this must be done before you power up the board, or the display output will not work.



Turn on, get the IP from the LCD (cable or wireless)
Log in as root, pass 1234, folow steps in the console
Log in as the user you created
apt update, apt upgrade
Turn on the internal PINs for ADXL345: https://www.klipper3d.org/RPi_microcontroller.html?h=gpio
Turn on the PINS via armbian-config > System > Hardware - toggle on the option there, confim and reboot
Install Klipper via: https://github.com/th33xitus/kiauh
