# Cross-compiler toolchain
CROSS_COMPILE = arm-linux-gnueabihf-
ARCH = arm

# Kernel source directory
#KERNEL_DIR = /path/to/bbb/kernel/headers

# Module name
MODULE_NAME = pchar

# Source files
SRC = $(MODULE_NAME).c

# Output directory
OBJDIR = /media/pritesh/BEAGLEBONE


# Default target
all: $(OBJDIR) $(OBJDIR)/$(MODULE_NAME).ko

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(OBJDIR)/$(MODULE_NAME).ko: $(SRC)
	$(MAKE) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KERNEL_DIR) M=$(PWD) modules

# Clean up
clean:
	rm -rf $(OBJDIR) *.o *.mod.c *.mod *.order *.symvers *.ko .*.cmd *.tmp_versions

# Prepare for module
modules_prepare:
	$(MAKE) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KERNEL_DIR) modules_prepare

# Target for installing the module on the BBB (requires SSH setup)
install: $(OBJDIR)/$(MODULE_NAME).ko
	scp $(OBJDIR)/$(MODULE_NAME).ko user@beaglebone:/lib/modules/$(shell uname -r)/extra
	ssh user@beaglebone 'depmod -a && modprobe $(MODULE_NAME)'

.PHONY: all clean modules_prepare install
