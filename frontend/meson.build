# SPDX-FileCopyrightText: 2023 Amyspark <amy@amyspark.me>
# SPDX-License-Identifier: BSD-3-Clause

faad_exe_srcs = files(
	'mp4read.c',
	'audio.c',
	'main.c',
	'unicode_support.c',
)

faad_exe_srcs += [config_h]

faad_exe_headers = files(
	'audio.h',
	'mp4read.h',
	'unicode_support.h',
)

if not cdata.has('HAVE_GETOPT_LONG')
	faad_exe_headers += files(
		'getopt.h',
	)
endif

faad_exe = executable(
	'faad',
	faad_exe_srcs,
	include_directories: base_includes,
	dependencies: faad2_dep,
	install: true
)

faad_man = configure_file(
	input: 'faad.man',
	output: 'faad.1',
	copy: true
)

install_man(faad_man)
