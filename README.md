# Build Linux ethercat

## Download the ethercat master source files

$ wget http://www.etherlab.org/download/ethercat/ethercat-1.5.2.tar.bz2

$ tar xjf ethercat-1.5.2.tar.bz2

## Download the usr folder  

$ sudo cp usr -rf /

## Download the Linux ethercat source files

$ git clone https://github.com/sittner/linuxcnc-ethercat.git linuxcnc-ethercat

## Add "#include <stdbool.h>" to file lcec_conf_util.c

$ sudo nano linuxcnc-ethercat/src/lcec_conf_util.c

## Building

$ cd linuxcnc-ethercat 

$ sudo make

$ sudo make install

# Test with EK1100, EL2042

Start EtherCAT Mater

sudo /etc/init.d/ethercat start

## Create file ethercat-conf.xml

<masters>
  
  <master idx="0" appTimePeriod="1000000" refClockSyncCycles="1000">
  
    <slave idx="0" type="EK1100" name="D1"/>
    
    <slave idx="1" type="EL2042" name="D2"/>
  
  </master>

</masters>

## Run halcmd

$ halrun

$ halcmd:loadrt trivkins

$ halcmd:loadrt motmod servo_period_nsec=1000000 num_joints=3

$ halcmd:loadusr -W lcec_conf /data/linuxcnc/hal/ethercat-conf.xml

$ halcmd:loadrt lcec



