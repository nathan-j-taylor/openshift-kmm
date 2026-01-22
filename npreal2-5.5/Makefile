KERNELRELEASE := $(shell uname -r)
NET_TIMEOUT := 10
TTYNAME := "ttyr"
POLLING_MODE := ""
REDHAT_ID := 7
OS_ID := ${REDHAT_ID}
K_MODULE_VERSION := $(shell uname -r)
K_RELEASE := $(shell echo ${K_MODULE_VERSION} | sed -e "s/-.*//g")
K_VERSION := $(shell echo ${K_RELEASE} | cut -d '.' -f 1)
K_PATCH_LEVEL := $(shell echo ${K_RELEASE} | cut -d '.' -f 2)
K_SUBLEVEL := $(shell echo ${K_RELEASE} | cut -d '.' -f 3)
K_VERSION_CODE := $(( (${K_VERSION}<<16)+(${K_PATCH_LEVEL}<<8)+${K_SUBLEVEL} ))
D_PATCH_VERSION := $(shell echo ${K_MODULE_VERSION} | awk -F '[-.]' '{print $$4}')
D_PATCH := ${D_PATCH_VERSION}

obj-m += npreal2.o

all:
	$(MAKE) -C /lib/modules/$(KERNELRELEASE)/build M=$$PWD EXTRA_CFLAGS="-DOS_TYPE=${OS_ID} -DDIS_PATCH=${D_PATCH_VERSION} -DTTYNAME='${TTYNAME}' -DNP_TIMEOUT=${NET_TIMEOUT}  " modules

clean:
	rm -r $(wildcard npreal2.mod.c npreal2.ko .tmp_versions \
	      Module.symvers Modules.symvers Module.markers modules.order \
	      $(foreach dir,./,$(addprefix $(dir),.*.cmd .*.o.flags *.o)))
