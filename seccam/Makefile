#
# by Akihabara Robot Community (MCU research div).
#
CXXSRC = $(shell find ./src -name "*.cxx")
CSRC   = $(shell find ./src -name "*.c")
OBJ    = $(CXXSRC:.cxx=.o) $(CSRC:.c=.o)
HXXSRC = $(shell find ./inc -name "*.hxx")
HSRC   = $(shell find ./inc -name "*.h")
TARGET = seccam

ifeq (,$(TOOLCHAIN_PREFIX))
$(error TOOLCHAIN_PREFIX is not set)
endif

ifeq (,$(CFLAGS))
$(error CFLAGS is not set)
endif

ifeq (,$(LDFLAGS))
$(error LDFLAGS is not set)
endif

CC = $(TOOLCHAIN_PREFIX)gcc
CXX = $(TOOLCHAIN_PREFIX)g++

CFLAGS += -std=c99 -Wall -Wextra -I$(SYSROOT)/usr/include -I./inc -I./lib/opencv-mobile-4.8.1-milkv-duo/include -I./lib/json/include -I./lib/cpp-httplib/include
CXXFLAGS += -std=c++14 -Wall -Wextra -I$(SYSROOT)/usr/include -I./inc -I./lib/opencv-mobile-4.8.1-milkv-duo/include -I./lib/json/include -I./lib/cpp-httplib/include

LDFLAGS += -pthread -L$(SYSROOT)/lib
LDFLAGS += -L$(SYSROOT)/usr/lib -L./lib/opencv-mobile-4.8.1-milkv-duo/lib
LIBS += -lc -lm -lstdc++ -lopencv_core

all: $(TARGET)

$(TARGET): $(OBJ)
	$(CC) $(LDFLAGS) -o $@ $^ $(LIBS)

%.o: %.c
	$(CC) -c $(CFLAGS) $(INCLUDE) -o $@ $<

%.o: %.cxx
	$(CXX) -c $(CXXFLAGS) $(INCLUDE) -o $@ $<

.PHONY: clean
clean:
	@rm *.o -rf
	@rm $(OBJ) -rf
	@rm $(TARGET)

