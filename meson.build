project('sgug-fam',
	 'cpp', 'c',
	 version : '0.1.0',
	 default_options : ['buildtype=release'])

version = meson.project_version().split('.')
install_major_version = version[0].to_int()
install_minor_version = version[1].to_int()
install_micro_version = version[2].to_int()

install_interface_age = 1
install_binary_age = 10000 * install_major_version + 100 * install_minor_version + 10 + install_micro_version

#add_global_arguments('-D_SGI_SOURCE -D_SGI_MP_SOURCE -D_SGI_REENTRANT_FUNCTIONS', language : ['c','cpp'])
add_global_arguments('-D_SGI_MP_SOURCE -D_SGI_REENTRANT_FUNCTIONS', language : ['c','cpp'])

install_prefix = get_option('prefix')
install_libdir = join_paths(install_prefix, get_option('libdir'))

install_soversion = 0
current = install_binary_age - install_interface_age
install_libversion = '@0@.@1@.@2@'.format(install_soversion, current, install_interface_age)

pkgconfig = import('pkgconfig')

inc = include_directories('src')

cc=meson.get_compiler('c')
cxx=meson.get_compiler('cpp')

lib_dependencies = [
]

lib_sources = files(
	    'src/btree.hpp',
	    'src/client.cpp',
	    'src/client.hpp',
	    'src/fam.cpp',
)

libfam = library('fam',
       sources: lib_sources,
       soversion: install_soversion,
       version: install_libversion,
       install: true,
       dependencies: lib_dependencies,
)

pkgconfig.generate(libfam,
  name: 'SGUG Fam',
  description: 'SGUG File Alteration Monitoring',
  filebase: 'fam',
)
