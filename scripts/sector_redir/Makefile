CC=arm-vita-eabi-gcc
FW=365
CFLAGS=-Os -fno-builtin-printf -fPIC -fno-builtin-memset -Wall -Wextra -Wno-unused-variable -DFW_$(FW)
OBJCOPY=arm-vita-eabi-objcopy
LDFLAGS=-nodefaultlibs -nostdlib

.PHONY: all clean

all: sector_int2ext_$(FW).e2xp sector_int2ext_$(FW)_full.e2xp

clean:
	rm -f *.o sector_int2ext_$(FW)_full.e2xp sector_int2ext_$(FW)_full sector_int2ext_$(FW).e2xp sector_int2ext_$(FW)

sector_int2ext_full.o: sector_int2ext.c
	$(CC) -c $^ -o $@ $(CFLAGS) -DFULL_REDIR

sector_int2ext_$(FW).e2xp: sector_int2ext_$(FW)
	$(OBJCOPY) -O binary $^ $@
	
sector_int2ext_$(FW): sector_int2ext.o
	$(CC) -o $@ $^ $(LDFLAGS) -T sector_int2ext.x

sector_int2ext_$(FW)_full.e2xp: sector_int2ext_$(FW)_full
	$(OBJCOPY) -O binary $^ $@
	
sector_int2ext_$(FW)_full: sector_int2ext_full.o
	$(CC) -o $@ $^ $(LDFLAGS) -T sector_int2ext.x
