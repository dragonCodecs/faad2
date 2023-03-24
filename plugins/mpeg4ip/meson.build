# SPDX-FileCopyrightText: 2023 Amyspark <amy@amyspark.me>
# SPDX-License-Identifier: BSD-3-Clause

faad2_plugins_srcs = files(
	'faad2.cpp',
	'aa_file.cpp',
)

faad2_plugin_args = [
	'-D_REENTRANT',
	'-DNOCONTROLS',
]

if compiler.get_argument_syntax() == 'msvc'
	faad2_plugin_args += '-EHs'
else
	faad2_plugin_args += '-fexceptions'
endif

faad2_plugin = shared_module(
	'faad2_plugin',
	faad2_plugins_srcs,
	cpp_args: faad2_plugin_args,
	dependencies: [m, faad2_dep],
	install: true,
	install_dir: get_option('mpeg4ip_player_plugin_dir')
)
