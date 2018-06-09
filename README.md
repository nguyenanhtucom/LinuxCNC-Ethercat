##Download the ethercat master source files

$ wget http://www.etherlab.org/download/ethercat/ethercat-1.5.2.tar.bz2

$ tar xjf ethercat-1.5.2.tar.bz2

## Download the usr folder  

$ sudo cp usr -rf /

## Download the Linux ethercat source files

$ git clone https://github.com/sittner/linuxcnc-ethercat.git linuxcnc-ethercat

# Add "#include <stdbool.h>" to file lcec_conf_util.c

$ sudo nano linuxcnc-ethercat/src/lcec_conf_util.c

## Building

$ cd linuxcnc-ethercat 

$ sudo make

$ sudo make install

