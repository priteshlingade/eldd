
obj-m = pchar.o

modules:
	make -C /lib/modules/`uname -r`/build M=`pwd` modules

cross:
	make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -C /home/pritesh/Desktop/linux/ M=`pwd` modules

bb:
	cd /media/pritesh/BEAGLEBONE

run:
	make ssh debian@192.168.6.2

clean:
	make -C /lib/modules/`uname -r`/build M=`pwd` clean

.phony : clean
