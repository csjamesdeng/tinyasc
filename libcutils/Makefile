TARGET = libcutils.a
INSTALL_DIR = ../lib

# TARGET_ARCH := arm
TARGET_CPU_SMP := false

# Omits atomic.c.arm, ashmem-dev.c debugger.c uevent.c
SRCS += \
	hashmap.c \
	native_handle.c \
	socket_inaddr_any_server.c \
	socket_local_client.c \
	socket_local_server.c \
	socket_loopback_client.c \
	socket_loopback_server.c \
	socket_network_client.c \
	sockets.c \
	config_utils.c \
	cpu_info.c \
	load_file.c \
	list.c \
	open_memstream.c \
	strdup16to8.c \
	strdup8to16.c \
	record_stream.c \
	process_name.c \
	threads.c \
	sched_policy.c \
	iosched_policy.c \
	str_parms.c \
	android_reboot.c \
	klog.c \
	partition_utils.c \
	properties.c \
	qtaguid.c \
	trace.c \

CC = $(CROSS_COMPILE)gcc
AR = $(CROSS_COMPILE)ar

ifeq ($(TARGET_ARCH),arm)
SRCS +=	arch-arm/memset32.S
else  # !arm
ifeq ($(TARGET_ARCH_VARIANT),x86-atom)
CFLAGS += -DHAVE_MEMSET16 -DHAVE_MEMSET32
SRCS += arch-x86/android_memset16.S arch-x86/android_memset32.S memory.c
else # !x86-atom
ifeq ($(TARGET_ARCH),mips)
SRCS += arch-mips/android_memset.c
else # !mips
SRCS += memory.c
endif # !mips
endif # !x86-atom
endif # !arm

ifeq ($(TARGET_CPU_SMP),true)
CFLAGS += -DANDROID_SMP=1
else
CFLAGS += -DANDROID_SMP=0
endif

CFLAGS += -I../include
CFLAGS += -DHAVE_PTHREADS

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
