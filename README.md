# Raspberry-AIS
Raspberry PI AIS Receiver for Ship tracking

*Work on:*
- Raspberry PI 3 B
- Raspberry PI 3 B+
- Raspberry PI 4

*Here's the code:*
- sudo apt-get update
- sudo apt-get upgrade
- sudo apt-get install git git-core cmake libusb-1.0-0-dev build-essential lsof

**install the RTL-2832U USB dongle driver**
- git clone https://git.osmocom.org/rtl-sdr
- cd rtl-sdr
- mkdir build
- cd build
- cmake ../ -DINSTALL_UDEV_RULES=ON
- make -j4
- sudo make install
- sudo ldconfig
- sudo ldconfig

**You should now do these steps to tell the system about what the new device is allowed to do, and reboot the system:**
- cd ~
- sudo cp ./rtl-sdr/rtl-sdr.rules /etc/udev/rules.d/
- sudo reboot
- rtl_test

**On most versions of Raspian except very early ones, you will need to "blacklist" the rtl2830 device to stop the OS using the DAB/TV drivers for the device.**
- cd /etc/modprobe.d
- sudo nano no-rtl.conf

**Add the following lines**
- blacklist dvb_usb_rtl28xxu
- blacklist rtl2832
- blacklist rtl2830

- sudo reboot
- rtl_test -t

**If you get error messages such as "cb transfer status: 1, canceling." it may be because the dongle is taking too much power from the Raspberry Pi.** 

*Let's Install AIS*
- sudo apt-get install update
- sudo apt-get install upgrade
- sudo apt install build-essential libtool automake autoconf librtlsdr-dev libfftw3-dev	
- git clone https://github.com/steve-m/kalibrate-rtl
- cd kalibrate-rtl/
- ./bootstrap && CXXFLAGS='-W -Wall -O3'
- ./configure
- make
- sudo make install	
- rtl_test -p

- kal -s 900 -g 49.6 -e 23

- kal -c 5 -g 49.6 -e 23

- cd ~
- git clone https://github.com/dgiardini/rtl-ais
- cd rtl-ais
- make
- ./rtl_ais -p 35 -n -h 192.168.1.15
**change with your PC IP**

*Thanks to:*
https://www.fontenay-ronan.fr/ais-receiver-on-a-raspberry-pi-with-rtl-sdr/
