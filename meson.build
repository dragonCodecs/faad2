# SPDX-FileCopyrightText: 2023 Amyspark <amy@amyspark.me>
# SPDX-License-Identifier: BSD-3-Clause

project(
	'faad2',
	'c', 'cpp',
	version: '2.10.1',
	license: 'GPL-2.0-or-later',
	default_options: [
		'c_std=c99',
	],
	meson_version: '>=0.56.0',
)

compiler = meson.get_compiler('c')

cdata = configuration_data()

add_project_arguments(
	'-DHAVE_CONFIG_H',
	'-DPACKAGE_VERSION="@0@"'.format(meson.project_version()),
	language: ['c', 'cpp']
)

if compiler.has_header('stdlib.h') and compiler.has_header('string.h')
	cdata.set10('STDC_HEADERS', true)
endif

if target_machine.system() == 'windows'
	add_project_arguments(
		'-D_CRT_SECURE_NO_WARNINGS',
		language: ['c', 'cpp']
	)
endif

header_macros = [
	['stdint.h', 'HAVE_STDINT_H'],
	['inttypes.h', 'HAVE_INTTYPES_H'],
	# The commented out includes are unused/used unchecked
	# ['mathf.h', 'HAVE_MATHF_H'],
	# ['float.h', 'HAVE_FLOAT_H'],
	# ['sys/time.h', 'HAVE_SYS_TIME_H'],
	['sys/stat.h', 'HAVE_SYS_STAT_H'],
	['sys/types.h', 'HAVE_SYS_TYPES_H'],
	['limits.h', 'HAVE_LIMITS_H'],
	['limits.h', 'HAVE_LIMITS_H'],
	# ['sysfs/libsysfs.h', 'HAVE_SYSFS_LIBSYSFS_H'],
]

foreach header : header_macros
	if compiler.has_header(header[0])
		cdata.set10(header[1], true)
	endif
endforeach

function_macros = [
	['strchr', 'HAVE_STRCHR'],
	['memcpy', 'HAVE_MEMCPY'],
	# ['getpwuid', 'HAVE_GETPWUID'],
	# ['strsep', 'HAVE_STRSEP'],
	['getopt_long', 'HAVE_GETOPT_LONG'],
]

foreach function : function_macros
	if compiler.has_function(function[0])
		cdata.set10(function[1], true)
	endif
endforeach

if compiler.has_header_symbol('math.h', 'lrintf')
	cdata.set10('HAVE_LRINTF', true)
endif

if compiler.has_type('float32_t', 
	prefix: '''#include <sys/types.h>
		#include <sys/float.h>'''
	)
	cdata.set10('HAVE_FLOAT32_T', true)
endif

thread_dep = dependency('threads', required: false)

m = compiler.find_library('m', required: false)

with_mpeg4ip = get_option('mpeg4ip')
if with_mpeg4ip
	external_mp4v2 = find_program('mpeg4ip-config', required: false)

	if external_mp4v2.found()
		cdata.set10('HAVE_MPEG4IP_PLUG', true)
		message('Building MPEG4IP plugin')
	else
		warning('MPEG4IP libmp4v2 is required for MPEG4IP plugin')
	endif
endif

with_drm = get_option('drm')
if with_drm
	cdata.set10('DRM', true)
	cdata.set10('DRM_PS', true)
endif

with_drc = get_option('drc')
if with_drc
	cdata.set10('APPLY_DRC', true)
endif

config_h = configure_file(
	output: 'config.h',
	configuration: cdata,
)

base_includes = include_directories('.')

subdir('include')
subdir('libfaad')
subdir('plugins')
subdir('docs')
subdir('frontend')
