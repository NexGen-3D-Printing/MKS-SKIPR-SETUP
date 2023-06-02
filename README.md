# MKS-CANBUS
Setting Up CANBUS ON the SKIPR and THR

Download the image file fome here: https://github.com/redrathnure/armbian-mkspi/releases

Install in the SD Card or eMMC via Rufus: https://rufus.ie/en/

Check the size of the system partition, maybe you need to rezise it, (leave 500MB free at the end).
Turn on, get the IP from the LCD (cable or wireless)
Log in as root, pass 1234, folow steps in the console
Log in as the user you created
apt update, apt upgrade
Turn on the internal PINs for ADXL345: https://www.klipper3d.org/RPi_microcontroller.html?h=gpio
Turn on the PINS via armbian-config > System > Hardware - toggle on the option there, confim and reboot
Install Klipper via: https://github.com/th33xitus/kiauh
