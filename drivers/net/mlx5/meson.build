# SPDX-License-Identifier: BSD-3-Clause
# Copyright 2018 6WIND S.A.
# Copyright 2018 Mellanox Technologies, Ltd

if not is_linux
	build = false
	reason = 'only supported on Linux'
	subdir_done()
endif

allow_experimental_apis = true
deps += ['hash', 'common_mlx5']
sources = files(
	'mlx5.c',
	'mlx5_ethdev.c',
	'mlx5_flow.c',
	'mlx5_flow_meter.c',
	'mlx5_flow_dv.c',
	'mlx5_flow_verbs.c',
	'mlx5_mac.c',
	'mlx5_mr.c',
	'mlx5_rss.c',
	'mlx5_rxmode.c',
	'mlx5_rxq.c',
	'mlx5_rxtx.c',
	'mlx5_mp.c',
	'mlx5_stats.c',
	'mlx5_trigger.c',
	'mlx5_txq.c',
	'mlx5_vlan.c',
	'mlx5_utils.c',
)
if (dpdk_conf.has('RTE_ARCH_X86_64')
	or dpdk_conf.has('RTE_ARCH_ARM64')
	or dpdk_conf.has('RTE_ARCH_PPC_64'))
	sources += files('mlx5_rxtx_vec.c')
endif
cflags_options = [
	'-std=c11',
	'-Wno-strict-prototypes',
	'-D_BSD_SOURCE',
	'-D_DEFAULT_SOURCE',
	'-D_XOPEN_SOURCE=600'
]
foreach option:cflags_options
	if cc.has_argument(option)
		cflags += option
	endif
endforeach
if get_option('buildtype').contains('debug')
	cflags += [ '-pedantic', '-UNDEBUG', '-DPEDANTIC' ]
else
	cflags += [ '-DNDEBUG', '-UPEDANTIC' ]
endif
