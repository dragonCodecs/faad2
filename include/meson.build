# SPDX-FileCopyrightText: 2023 Amyspark <amy@amyspark.me>
# SPDX-License-Identifier: BSD-3-Clause

libfaad_headers = files(
	'neaacdec.h',
)

libfaad_includes = include_directories('.')

faac_h = configure_file(
	input: 'faad.h.in',
	output: 'faad.h',
	configuration: {
		'VERSION': meson.project_version(),
	}
)

libfaad_headers += faac_h
