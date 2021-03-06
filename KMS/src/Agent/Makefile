################################################################
# Makefile
#
# Copyright 2015 hbwoo
#
#  This file is part of TrustKeystoreAgent

#compile option
export ARC = -m32
export OPT = -Os -fPIC -fvisibility=hidden -ffunction-sections -fdata-sections -m32
export LD = ld -melf_i386
export TEST_OPT = -DTEST_TKS_AGENT

TARGET_TrustKeystoreAgent = libTrustKeystoreAgent.so
TARGET_TKSAgent = libTKSAgent.so
TARGET_TKSAgentAdv = libTKSAgentAdv.so
TARGET_TKSAgentLite = libTKSAgentLite.so
TARGET_JniTKSAgentAdv = libJniTKSAgentAdv.so

OBJ_TrustKeystoreAgent = TrustKeystoreAgent/built-in.o
OBJ_TKSAgent = TKSAgent/built-in.o
OBJ_TKSAgentAdv = TKSAgentAdv/built-in.o
OBJ_TKSAgentLite = TKSAgentLite/built-in.o
OBJ_JniTKSAgentAdv = JniTrustKeystoreAgent/built-in.o

SUBDIRS = sqlite3 \
			libexpat \
			wolfssl-3.4.6/src \
			wolfssl-3.4.6/wolfcrypt/src \
			TrustKeystoreAgent \
			TKSAgent \
			TKSAgentAdv \
			TKSAgentLite \
			JniTrustKeystoreAgent \
			TestAgent

OBJS = sqlite3/built-in.o \
			libexpat/built-in.o \
			wolfssl-3.4.6/src/built-in.o \
			wolfssl-3.4.6/wolfcrypt/src/built-in.o
			#TrustKeystoreAgent/built-in.o
			#TestAgent/built-in.o \
			
STATIC_LIBS = -libsqlite3\
			-libexpat\
			-libwolfssl\
			-libwolfcrypt
			
STATIC_LIB_DIRS = -L./sqlite3\
	-L./libexpat\
	-L./wolfssl-3.4.6/src\
	-L./wolfssl-3.4.6/wolfcrypt/src
	

all : compile $(OBJS) $(OBJ_TrustKeystoreAgent) $(OBJ_TKSAgent) $(OBJ_TKSAgentAdv) $(OBJ_TKSAgentLite)
	$(CC) $(OPT) -shared -W1,-soname,$(TARGET_TrustKeystoreAgent) -o $(TARGET_TrustKeystoreAgent) $(OBJS) $(OBJ_TrustKeystoreAgent) -Wl,--gc-sections,-s -lpthread -lm
	$(CC) $(OPT) -shared -W1,-soname,$(TARGET_TKSAgent) -o $(TARGET_TKSAgent) $(OBJS) $(OBJ_TKSAgent) -Wl,--gc-sections,-s -lpthread -lm
	$(CC) $(OPT) -shared -W1,-soname,$(TARGET_TKSAgentAdv) -o $(TARGET_TKSAgentAdv) $(OBJS) $(OBJ_TKSAgentAdv) -Wl,--gc-sections,-s -lpthread -lm
	$(CC) $(OPT) -shared -W1,-soname,$(TARGET_TKSAgentLite) -o $(TARGET_TKSAgentLite) $(OBJS) $(OBJ_TKSAgentLite) -Wl,--gc-sections,-s -lpthread -lm
	$(CC) $(OPT) -shared -W1,-soname,$(TARGET_JniTKSAgentAdv) -o $(TARGET_JniTKSAgentAdv) $(OBJ_JniTKSAgentAdv) $(OBJS) $(OBJ_TKSAgentAdv) -Wl,--gc-sections,-s -lpthread -lm
	#$(CC) $(OPT) -ldl -o test TestAgent/built-in.o -L./ -lTrustKeystoreAgent
	$(CC) $(OPT) -ldl -o test TestAgent/built-in.o -L./ -lTKSAgent
	
compile :
	@for dir in $(SUBDIRS); do \
	make -C $$dir || exit $?; \
	done

clean :
	@for dir in $(SUBDIRS); do \
	make -C $$dir clean; \
	done
	rm -rf *.o *.i *.s $(TARGET)
