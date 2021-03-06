# SPDX-License-Identifier: BSD-3-Clause
# Copyright 2020 Mellanox Technologies, Ltd

include $(RTE_SDK)/mk/rte.vars.mk

# Library name.
LIB = librte_pmd_mlx5_regex.a

# Sources.
SRCS-$(CONFIG_RTE_LIBRTE_MLX5_REGEX_PMD) += mlx5.c
SRCS-$(CONFIG_RTE_LIBRTE_MLX5_REGEX_PMD) += mlx5_regex.c

# Basic CFLAGS.
CFLAGS += -O3
CFLAGS += -std=c11 -Wall -Wextra
CFLAGS += -g
CFLAGS += -I$(RTE_SDK)/drivers/common/mlx5
CFLAGS += -I$(RTE_SDK)/lib/librte_regexdev
CFLAGS += -I$(BUILDDIR)/drivers/common/mlx5
CFLAGS += -D_BSD_SOURCE
CFLAGS += -D_DEFAULT_SOURCE
CFLAGS += -D_XOPEN_SOURCE=600
CFLAGS += $(WERROR_FLAGS)
CFLAGS += -Wno-strict-prototypes
LDLIBS += -lrte_common_mlx5
LDLIBS += -lm
LDLIBS += -lrte_eal -lrte_mbuf
LDLIBS += -lrte_kvargs
LDLIBS += -lrte_bus_pci
LDLIBS += -lrte_regexdev

# A few warnings cannot be avoided in external headers.
CFLAGS += -Wno-error=cast-qual

EXPORT_MAP := rte_pmd_mlx5_regex_version.map

# memseg walk is not part of stable API
CFLAGS += -DALLOW_EXPERIMENTAL_API

# DEBUG which is usually provided on the command-line may enable
# CONFIG_RTE_LIBRTE_MLX5_DEBUG.
ifeq ($(DEBUG),1)
CONFIG_RTE_LIBRTE_MLX5_DEBUG := y
endif

# User-defined CFLAGS.
ifeq ($(CONFIG_RTE_LIBRTE_MLX5_DEBUG),y)
CFLAGS += -pedantic -UNDEBUG
ifneq ($(CONFIG_RTE_TOOLCHAIN_ICC),y)
CFLAGS += -DPEDANTIC
endif
AUTO_CONFIG_CFLAGS += -Wno-pedantic
else
CFLAGS += -DNDEBUG -UPEDANTIC
endif

include $(RTE_SDK)/mk/rte.lib.mk

