# This file is part of the Black Magic Debug project.
#
# Copyright (C) 2023 1BitSquared <info@1bitsquared.com>
# Written by Rafael Silva <perigoso@riseup.net>
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
# 1. Redistributions of source code must retain the above copyright notice, this
#    list of conditions and the following disclaimer.
#
# 2. Redistributions in binary form must reproduce the above copyright notice,
#    this list of conditions and the following disclaimer in the documentation
#    and/or other materials provided with the distribution.
#
# 3. Neither the name of the copyright holder nor the names of its
#    contributors may be used to endorse or promote products derived from
#    this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
# CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
# OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

bmd_core_includes = include_directories(
	'.',
	'include',
)

bmd_core_sources = files(
	'command.c',
	'crc32.c',
	'exception.c',
	'gdb_hostio.c',
	'gdb_main.c',
	'gdb_packet.c',
	'hex_utils.c',
	'main.c',
	'maths_utils.c',
	'morse.c',
	'remote.c',
	'timing.c',
)

bmd_core_args = []

# Debug output handling
if (get_option('debug_output'))
	bmd_core_args += ['-DENABLE_DEBUG=1']
endif

# RTT support handling
if get_option('rtt_support')
	bmd_core_sources += files('rtt.c')
	bmd_core_args += ['-DENABLE_RTT=1']

	rtt_ident = get_option('rtt_ident')
	if rtt_ident != ''
		bmd_core_args += [f'-DRTT_IDENT=@rtt_ident@']
	endif
endif

# Get BMD targets dependency
subdir('target')

# Core BMD "library" (a dependency with all sources and flags to build the BMD core)
bmd_core = declare_dependency(
	compile_args: bmd_core_args,
	include_directories: bmd_core_includes,
	sources: [bmd_core_sources, version],
	dependencies: bmd_targets,
)

# Get probe host and platform dependencies
# TODO: when support for build as a host library is added, this can be conditional?
subdir('platforms')