# 1. 架构选择（默认x86）
ARCH ?= x86
TARGET = dry

# 2. 编译器配置
ifeq ($(ARCH), x86)
    CC = gcc             # x86使用标准gcc 
else
    CC = aarch64-linux-gnu-gcc  # ARM64使用交叉编译器
endif

# 3. 目录定义
# 定义项目根目录（Makefile所在路径）
ROOT_DIR  := $(patsubst %/,%,$(dir $(abspath $(lastword $(MAKEFILE_LIST)))))
ROOT_DIR  := $(strip $(ROOT_DIR))
SRC_DIR   := $(ROOT_DIR)
INC_DIR   := $(ROOT_DIR)
BUILD_DIR := $(ROOT_DIR)/build_$(ARCH)
OUTPUT_DIR:= $(ROOT_DIR)/bin_$(ARCH)

$(warning OUTPUT_DIR=$(OUTPUT_DIR)) 

# 5. 编译参数
CFLAGS = 
LDFLAGS = -DPASS2 -static

# 6. 核心规则
all: $(OUTPUT_DIR)/$(TARGET)

$(OUTPUT_DIR)/$(TARGET): $(SRC_DIR)/dry.c  $(BUILD_DIR)/dry1.o 
	@echo test = $(OUTPUT_DIR)/$(TARGET)
	@mkdir -p $(OUTPUT_DIR)
	
#	echo $(CC) $^ -o $@ $(LDFLAGS)
	$(CC) $^ -o $@ $(LDFLAGS)

$(BUILD_DIR)/dry1.o: $(SRC_DIR)/dry.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c $< -o $@ 

# 7. 清理规则
clean:
	rm -rf $(BUILD_DIR) $(OUTPUT_DIR)
distclean:
	rm -rf $(ROOT_DIR)/build_* $(ROOT_DIR)/bin_*
