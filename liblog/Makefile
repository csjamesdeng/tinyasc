TARGET = liblog.a
INSTALL_DIR = ../lib

SRCS += \
	logd_write.c \
	uio.c

CC = $(CROSS_COMPILE)gcc
AR = $(CROSS_COMPILE)ar

CFLAGS := -I../include

OBJS = $(SRCS:.c=.o)

all: $(TARGET)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(TARGET): $(OBJS)
	$(AR) r $@ $(OBJS)
	[ -f $(INSTALL_DIR) ] || mkdir -p $(INSTALL_DIR)
	cp $(TARGET) $(INSTALL_DIR)

.PHONY: clean
clean:
	rm -rf $(OBJS) $(TARGET)
