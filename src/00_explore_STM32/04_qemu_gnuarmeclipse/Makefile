CROSS_COMPILE = arm-linux-gnueabihf
# Platform: ARM Cortex-M3
arch    ?= arm
CC      := $(CROSS_COMPILE)-gcc
# CC      := arm-linux-gnueabihf-gcc-5
LD      := $(CROSS_COMPILE)-ld
OBJCOPY := $(CROSS_COMPILE)-objcopy
DD      := $(CROSS_COMPILE)-dd
# QEMU    := qemu-system-arm
# QEMU    := qemu-arm-static
QEMU_PATH := /opt/gnuarmeclipse/qemu/2.8.0-201703022210-head/bin/qemu-system-gnuarmeclipse
QEMU_Cortex := $(QEMU_PATH)
GDB     := gdb

# myboard ?= STM32-H103 
 myboard ?=  STM32F4-Discovery
CFLAGS := -static -Wall -fno-stack-protector


.PHONY: build clean run 

asm_obj := $(patsubst src/%.s,\
	build/arch/$(arch)/%.elf, $(wildcard src/*.s))

build/arch/$(arch)/%.elf : src/%.s
	mkdir -p $(shell dirname $@)
	$(CC) $(CFLAGS) $< -o $@  



run: $(asm_obj)
	@echo "result:"
	$(QEMU_Cortex) -board $(myboard) --image $(asm_obj)

qemu: $(asm_obj)
	@echo "result:"
	$(QEMU_Cortex) -board $(myboard) $(asm_obj)

build: 
	$(CC) $(CFLAGS) src/hello_arm.s -o $(asm_obj)

clean:
	@# rm -r build
	@if [ ! -d "build" ];then \
	echo "directory 'build' currently does NOT exist."; \
	else \
	rm -r build; \
	fi
