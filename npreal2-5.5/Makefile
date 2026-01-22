KERNELRELEASE := $(shell uname -r)

obj-m += npreal2.o

all:
	$(MAKE) -C /lib/modules/$(KERNELRELEASE)/build M=$$PWD modules

clean:
	rm -r $(wildcard npreal2.mod.c npreal2.ko .tmp_versions \
	      Module.symvers Modules.symvers Module.markers modules.order \
	      $(foreach dir,./,$(addprefix $(dir),.*.cmd .*.o.flags *.o)))
