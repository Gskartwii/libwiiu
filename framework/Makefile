CC=powerpc-eabi-gcc
CFLAGS=-nostdinc -fno-builtin -c
LD=powerpc-eabi-ld
LDFLAGS=-Ttext 1800000 --oformat binary

root:=$(CURDIR)
project	:=	$(root)/src
build	:=	 $(root)/bin
all: setup findcode500 findcode410 findcode400
setup:
	mkdir -p $(root)/bin
findcode500:
ifeq ("$(wildcard $(build)/findcode500.bin)","")
	# Build findcode
	$(CC) $(CFLAGS) -DVER=500+ $(project)/findcode500.c
	#-Wa,-a,-ad
	cp -r $(root)/findcode500.o $(build)
	rm $(root)/findcode500.o
	$(LD) $(LDFLAGS) -o $(build)/findcode500.bin $(build)/findcode500.o
	# Get rid of GCC function prologue and move stack out of our buffer
	# Result should start with: 94 21 E0 00 7C 3F 0B 78 3D 20 1D D7 61 29 B8 14
	dd if=$(build)/findcode500.bin of=$(build)/findcode500.bin bs=4 obs=4 skip=5 count=1 conv=notrunc
	dd if=$(build)/findcode500.bin of=$(build)/findcode500.bin bs=4 obs=4 skip=4 seek=1 count=1 conv=notrunc
	dd if=$(build)/findcode500.bin of=$(build)/findcode500.bin bs=4 obs=4 skip=6 seek=2 conv=notrunc

	dd if=$(build)/findcode500.bin of=$(build)/stack500.bin obs=432 seek=1 conv=notrunc
endif
findcode410:
ifeq ("$(wildcard $(build)/findcode410.bin)","")
	# Build findcode
	$(CC) $(CFLAGS) -DVER=410+ $(project)/findcode410.c
	#-Wa,-a,-ad
	cp -r $(root)/findcode410.o $(build)
	rm $(root)/findcode410.o
	$(LD) $(LDFLAGS) -o $(build)/findcode410.bin $(build)/findcode410.o
	# Get rid of GCC function prologue and move stack out of our buffer
	# Result should start with: 94 21 E0 00 7C 3F 0B 78 3D 20 1D D7 61 29 B8 14
	dd if=$(build)/findcode410.bin of=$(build)/findcode410.bin bs=4 obs=4 skip=5 count=1 conv=notrunc
	dd if=$(build)/findcode410.bin of=$(build)/findcode410.bin bs=4 obs=4 skip=4 seek=1 count=1 conv=notrunc
	dd if=$(build)/findcode410.bin of=$(build)/findcode410.bin bs=4 obs=4 skip=6 seek=2 conv=notrunc
	dd if=$(build)/findcode410.bin of=$(build)/stack410.bin obs=432 seek=1 conv=notrunc
endif
findcode400:
ifeq ("$(wildcard $(build)/findcode400.bin)","")
	# Build findcode
	$(CC) $(CFLAGS) -DVER=400+ $(project)/findcode400.c
	#-Wa,-a,-ad
	cp -r $(root)/findcode400.o $(build)
	rm $(root)/findcode400.o
	$(LD) $(LDFLAGS) -o $(build)/findcode400.bin $(build)/findcode400.o
	# Get rid of GCC function prologue and move stack out of our buffer
	# Result should start with: 94 21 E0 00 7C 3F 0B 78 3D 20 1D D7 61 29 B8 14
	dd if=$(build)/findcode400.bin of=$(build)/findcode400.bin bs=4 obs=4 skip=5 count=1 conv=notrunc
	dd if=$(build)/findcode400.bin of=$(build)/findcode400.bin bs=4 obs=4 skip=4 seek=1 count=1 conv=notrunc
	dd if=$(build)/findcode400.bin of=$(build)/findcode400.bin bs=4 obs=4 skip=6 seek=2 conv=notrunc
	#Differen't on 400
	dd if=$(build)/findcode400.bin of=$(build)/stack400.bin obs=352 seek=1 conv=notrunc
endif
clean:
	rm -r $(build)/*
