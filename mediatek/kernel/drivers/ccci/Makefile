#CONFIG_MTK_CCCI_DRIVER :=m
ifneq ($(filter-out MT8320,$(MTK_PLATFORM)),)

include $(MTK_ROOT_BUILD)/Makefile
#CCCI_PLATFORM_DRIVER_DIR :=  $(wildcard $(obj)/$(call to-root,$(obj))mediatek/platform/$(call lc,\
#                               $(MTK_PLATFORM))/kernel/drivers/ccci)
CCCI_PLATFORM_DRIVER_DIR :=  $(srctree)/mediatek/platform/$(call lc,$(MTK_PLATFORM))/kernel/drivers/ccci
ifeq ($(CCCI_PLATFORM_DRIVER_DIR),)
$(error Invalid ccci platform path, please check)
endif


obj-$(CONFIG_MTK_CCCI_DRIVER) += ccci.o
ccci-y :=ccci_init.o
ccci-y +=ccci_hw.o ccci_logical.o ccci_chrdev.o 
ccci-y +=ccci_md_main.o 
ccci-y +=ccci_tty.o
ccci-y +=ccci_ipc.o
ccci-y +=ccci_pmic.o
ccci-y +=ccci_fs_main.o
ccci-y +=ccci_rpc_main.o

#include $(CCCI_PLATFORM_DRIVER_DIR)/Makefile



clean-files += $(patsubst $(obj)/%,%,$(wildcard $(obj)/*~))

ccflags-y  += -I$(srctree)/../bionic/libc/kernel/common/linux  -I$(srctree)/$(obj)/include  -I$(CCCI_PLATFORM_DRIVER_DIR)/include

ifneq ($(TARGET_BUILD_VARIANT),user)
#ccflags-y  += -DCCCI_DEBUG_ON -D__CCCI_LOG__  -DCCCI_MD_DEBUG_ON  #-save-temps
ccflags-y  += -DCCCI_DEBUG_ON  -DCCCI_MD_DEBUG_ON  #-save-temps
#ccflags-y  += -DENCRYPT_DEBUG -DCCCI_RPC_DEBUG_ON
endif
ccflags-y  += -D__CCCI_LOG__

ifdef CONFIG_ARCH_MT6573
ccflags-y += #-DCCCI_STATIC_SHARED_MEM
endif

else 
obj- :=dummy.o


endif
