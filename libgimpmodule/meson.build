
global_cflags = []
global_lflags = []

global_cflags += [
]

if platform_win32
  global_cflags += '-no-undefined'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  # global_lflags += ['-export-symbols', 'gimpmodule.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpModule' + '"',
  '-DGIMP_MODULE_COMPILATION',
]



libgimpmodule_sources = [
  'gimpmodule.c',
  'gimpmoduledb.c',
]

libgimpmodule_headers = [
  'gimpmodule.h',
  'gimpmoduledb.h',
  'gimpmoduletypes.h',
]


libgimpmodule = library('gimpmodule-'+ api_version,
  libgimpmodule_sources,
  include_directories: rootInclude,
  dependencies: [
    gio, glib, gmodule,
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, libgimpconfig, ],
)

install_headers(
  libgimpmodule_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpmodule'),
)


