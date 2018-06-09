# Build linuxcnc-ethercat

# You need file .h, .a, .la, . . . for build

    Download the file usr.tar.gz 
    $ tar xjf usr.tar.gz
    $ sudo cp usr -rf /
Or

    Build IgH-EtherCAT-Master (https://github.com/nguyenanhtucom/IgH-EtherCAT-Master)

    $ cd ethercat-1.5.2
    $ sudo cp include/ecrt.h  /usr/include
    $ sudo cp include/ectty.h  /usr/include
    $ sudo cp lib/.libs/libethercat.la /usr/lib
    $ sudo cp lib/.libs/libethercat.a /usr/lib
    $ sudo cp include/ecrt.h  /usr/realtime-3.4-9-rtai-686-pae/include
    $ sudo cp Module.symvers  /usr/realtime-3.4-9-rtai-686-pae/modules/ethercat

## Download the linux-ethercat source files

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

    halcmd:loadrt trivkins

    halcmd:loadrt motmod servo_period_nsec=1000000 num_joints=3

    halcmd:loadusr -W lcec_conf /data/linuxcnc/hal/ethercat-conf.xml

    halcmd:loadrt lcec



