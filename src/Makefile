SRC_DIR     = ./
LIB_DIR     = ../lib
OPENCM3_DIR = $(LIB_DIR)/libopencm3
MCU_FAMILY  = stm32f1
CORTEX_M    = 3
BINARY_NAME = main
LDSCRIPT    = $(OPENCM3_DIR)/lib/stm32/f1/stm32f103x8.ld
MAIN_START  = 0x8000000

BINARY          = $(SRC_DIR)/$(BINARY_NAME)
LIBNAME         = opencm3_$(shell echo $(MCU_FAMILY) | tr A-Z a-z)
DEFS           += -D$(shell echo $(MCU_FAMILY) | tr a-z A-Z)
FP_FLAGS       ?= -msoft-float
ARCH_FLAGS      = -mthumb -mcpu=cortex-m$(CORTEX_M) $(FP_FLAGS) -mfix-cortex-m$(CORTEX_M)-ldrd
OOCD           ?= openocd
OOCD_INTERFACE ?= flossjtag
OOCD_TARGET    ?= $(shell echo $(MCU_FAMILY) | tr A-Z a-z)x
OBJS           += $(foreach c_file, $(filter-out, $(BINARY_NAME).c, $(wildcard $(SRC_DIR)/*.c)), $(c_file:.c=.o))

.PHONY: all
all: $(BINARY).bin

burn: $(BINARY).bin
	st-flash write $< $(MAIN_START)

burn_dfu: $(BINARY).bin
	dfu-util -a 0 -d 0483:df11 -s $(MAIN_START):leave -D $<

include ./libopencm3.rules.mk
