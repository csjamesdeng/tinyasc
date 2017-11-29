TARGET = adbd
INSTALL_DIR = ../bin

SRCS := \
	adb.c \
	backup_service.c \
	fdevent.c \
	transport.c \
	transport_local.c \
	transport_usb.c \
	adb_auth_client.c \
	sockets.c \
	services.c \
	file_sync_service.c \
	jdwp_service.c \
	framebuffer_service.c \
	remount_service.c \
	usb_linux_client.c \
	log_service.c

CC = $(CROSS_COMPILE)gcc
LD = $(CROSS_COMPILE)ld

CFLAGS += -O2 -g -DADB_HOST=0 -Wall -Wno-unused-parameter
CFLAGS += -D_XOPEN_SOURCE -D_GNU_SOURCE
CFLAGS += -DALLOW_ADBD_ROOT=1
CFLAGS += -DHAVE_SYS_UIO_H
CFLAGS += -I../include

LDFLAGS += -lpthread -L../lib -lcutils -llog -lmincrypt

OBJS = $(SRCS:.c=.o)

all: $(TARGET)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(TARGET): $(OBJS)
	$(CC) $(OBJS) $(LDFLAGS) -o $@
	[ -f $(INSTALL_DIR) ] || mkdir -p $(INSTALL_DIR)
	cp $(TARGET) $(INSTALL_DIR)

.PHONY: clean
clean:
	rm -rf $(OBJS) $(TARGET)
