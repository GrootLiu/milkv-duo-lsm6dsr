SDK_DIR 	  = /path/to/duo-buildroot-sdk
CROSS_COMPILE = $(SDK_DIR)/host-tools/gcc/riscv64-linux-musl-x86_64/bin/riscv64-unknown-linux-musl-
KSRC		  = $(SDK_DIR)/linux_5.10/build/cv1800b_milkv_duo_sd
ARCH		  = riscv

all:
	$(MAKE) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KSRC) M=$(shell pwd)  modules
	$(CROSS_COMPILE)gcc lsm6dsr-app.c -o lsm6dsr-app -Wall -O2 -mcpu=c906fdv -march=rv64imafdcv0p7xthead -mcmodel=medany -mabi=lp64d -static

clean:
	$(MAKE) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KSRC) M=$(shell pwd)  modules clean
	rm -rf modules.order
	rm -rf lsm6dsr-app

obj-m += i2c-lsm6dsr.o
