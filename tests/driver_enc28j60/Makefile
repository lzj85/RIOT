include ../Makefile.tests_common

BOARD_INSUFFICIENT_MEMORY := arduino-duemilanove arduino-mega2560 arduino-nano \
                             arduino-uno msb-430 msb-430h nucleo-f334r8 \
                             nucleo-l053r8 nucleo-f031k6 nucleo-f042k6 \
                             nucleo-f303k8 nucleo-l031k6 mega-xplained \
                             stm32f0discovery telosb waspmote-pro wsn430-v1_3b \
                             wsn430-v1_4 z1

USEMODULE += auto_init_gnrc_netif
USEMODULE += enc28j60
USEMODULE += gnrc_ipv6_router_default
USEMODULE += gnrc_icmpv6_echo
USEMODULE += shell
USEMODULE += shell_commands
USEMODULE += ps

# set board specific peripheral configurations
ifneq (,$(filter stm32f4discovery,$(BOARD)))
  ENC_SPI ?= SPI_DEV\(1\)
  ENC_CS  ?= GPIO_PIN\(PORT_B,12\)
  ENC_INT ?= GPIO_PIN\(PORT_B,11\)
  ENC_RST ?= GPIO_PIN\(PORT_B,10\)
endif

# fallback: set SPI bus and pins to default values
ENC_SPI ?= SPI_DEV\(0\)
ENC_CS  ?= GPIO_PIN\(0,0\)
ENC_INT ?= GPIO_PIN\(0,1\)
ENC_RST ?= GPIO_PIN\(0,2\)
# export SPI and pins
CFLAGS += -DENC28J60_PARAM_SPI=$(ENC_SPI)
CFLAGS += -DENC28J60_PARAM_CS=$(ENC_CS)
CFLAGS += -DENC28J60_PARAM_INT=$(ENC_INT)
CFLAGS += -DENC28J60_PARAM_RESET=$(ENC_RST)

# make sure we read the local enc28j60 params file
CFLAGS += -I$(CURDIR)

include $(RIOTBASE)/Makefile.include
