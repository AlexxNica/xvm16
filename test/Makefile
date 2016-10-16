KERNEL := xvmtest.bin
IMG := xvmtest
LIB := target/i686-unknown-linux-gnu/release/libxvmtest.a
BOOT := boot.o
CROSS_PREFIX ?= i386-elf-

all: $(IMG)

$(IMG): $(KERNEL)
	$(CROSS_PREFIX)objcopy -j .text -j .data -O binary $< $@

$(KERNEL): $(LIB) $(BOOT) src/xvmtest.lds
	$(CROSS_PREFIX)ld -T src/xvmtest.lds -o $@ $(BOOT) $(LIB)

$(BOOT): src/boot.asm
	nasm -f elf32 -o $@ $<

$(LIB): cargo

cargo:
	cargo build --target i686-unknown-linux-gnu --release

clean:
	cargo clean
	rm -rf $(KERNEL) $(BOOT)

.PHONY: all cargo clean