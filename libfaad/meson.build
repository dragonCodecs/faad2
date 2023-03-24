# SPDX-FileCopyrightText: 2023 Amyspark <amy@amyspark.me>
# SPDX-License-Identifier: BSD-3-Clause

libfaad_srcs = files(
	'bits.c',
	'cfft.c',
	'decoder.c',
	'drc.c',
	'drm_dec.c',
	'error.c',
	'filtbank.c',
	'ic_predict.c',
	'is.c',
	'lt_predict.c',
	'mdct.c',
	'mp4.c',
	'ms.c',
	'output.c',
	'pns.c',
	'ps_dec.c',
	'ps_syntax.c',
	'pulse.c',
	'specrec.c',
	'syntax.c',
	'tns.c',
	'hcr.c',
	'huffman.c',
	'rvlc.c',
	'ssr.c',
	'ssr_fb.c',
	'ssr_ipqf.c',
	'common.c',
	'sbr_dct.c',
	'sbr_e_nf.c',
	'sbr_fbt.c',
	'sbr_hfadj.c',
	'sbr_hfgen.c',
	'sbr_huff.c',
	'sbr_qmf.c',
	'sbr_syntax.c',
	'sbr_tf_grid.c',
	'sbr_dec.c',
)

libfaad_srcs += [libfaad_headers, config_h]

libfaad_srcs_headers = files(
	'analysis.h',
	'bits.h',
	'cfft.h',
	'cfft_tab.h',
	'common.h',
	'drc.h',
	'drm_dec.h',
	'error.h',
	'fixed.h',
	'filtbank.h',
	'huffman.h',
	'ic_predict.h',
	'iq_table.h',
	'is.h',
	'kbd_win.h',
	'lt_predict.h',
	'mdct.h',
	'mdct_tab.h',
	'mp4.h',
	'ms.h',
	'output.h',
	'pns.h',
	'ps_dec.h',
	'ps_tables.h',
	'pulse.h',
	'rvlc.h',
	'sbr_dct.h',
	'sbr_dec.h',
	'sbr_e_nf.h',
	'sbr_fbt.h',
	'sbr_hfadj.h',
	'sbr_hfgen.h',
	'sbr_huff.h',
	'sbr_noise.h',
	'sbr_qmf.h',
	'sbr_syntax.h',
	'sbr_tf_grid.h',
	'sine_win.h',
	'specrec.h',
	'ssr.h',
	'ssr_fb.h',
	'ssr_ipqf.h',
	'ssr_win.h',
	'syntax.h',
	'structs.h',
	'tns.h',
	'sbr_qmf_c.h',
	'codebook/hcb.h',
	'codebook/hcb_1.h',
	'codebook/hcb_2.h',
	'codebook/hcb_3.h',
	'codebook/hcb_4.h',
	'codebook/hcb_5.h',
	'codebook/hcb_6.h',
	'codebook/hcb_7.h',
	'codebook/hcb_8.h',
	'codebook/hcb_9.h',
	'codebook/hcb_10.h',
	'codebook/hcb_11.h',
	'codebook/hcb_sf.h',
)

libfaad_link_args = []

libfaad_link_args += compiler.get_supported_link_arguments(
	'-no-undefined',
)

libfaad = library(
	'libfaad',
	libfaad_srcs,
	extra_files: libfaad_srcs_headers,
	include_directories: libfaad_includes,
	gnu_symbol_visibility: 'hidden',
	dependencies: m,
	link_args: libfaad_link_args,
	version: meson.project_version(),
	vs_module_defs: '../project/msvc/libfaad2.def',
	install: true,
)

if with_drm
	libfaad_drm_args = [
		'-DDRM_SUPPORT',
	]

	libfaad_drm = library(
		'libfaad_drm',
		libfaad_srcs,
		extra_files: libfaad_srcs_headers,
		c_args: libfaad_drm_args,
		include_directories: libfaad_includes,
		gnu_symbol_visibility: 'hidden',
		dependencies: m,
		link_args: libfaad_link_args,
		version: meson.project_version(),
		vs_module_defs: '../project/msvc/libfaad2.def',
		install: true,
	)
endif

faad2_dep = declare_dependency(
	link_with: libfaad,
	dependencies: m,
	include_directories: libfaad_includes,
)
meson.override_dependency('faad2', faad2_dep)

if with_drm
	faad2_drm_dep = declare_dependency(
		link_with: libfaad_drm,
		dependencies: m,
		include_directories: libfaad_includes,
	)
	meson.override_dependency('faad2_drm', faad2_drm_dep)
endif

pkg = import('pkgconfig')
pkg.generate(
	libfaad,
	name: 'FAAD2',
	description: 'Freeware Advanced Audio (AAC) Decoder',
)

install_headers(libfaad_headers)
