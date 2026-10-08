SRC_NAME = ipt2socks-fakedns-1.0.0
THISDIR = $(shell pwd)

# Upstream enables -flto=auto, but the Padavan GCC 7.4 toolchain was
# built without LTO support. Keep the ipt2socks build flow and only
# override the incompatible compiler and linker flags.
all: extract_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME) \
		CC="$(CC)" \
		CFLAGS="$(CFLAGS) -std=c99 -pthread -fno-strict-aliasing -ffunction-sections -fdata-sections" \
		LDFLAGS="$(LDFLAGS) -pthread -Wl,--gc-sections"

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar -xf $(SRC_NAME).tar ; \
	fi )

clean:
	rm -rf $(SRC_NAME)

romfs:
	$(ROMFSINST) -p +x $(THISDIR)/$(SRC_NAME)/build/release/ipt2socks /usr/bin/ipt2socks
