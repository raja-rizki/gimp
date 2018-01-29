
libgimpmodule_sources = [
  'gimpmodule.c',
  'gimpmoduledb.c',
]

libgimpmodule_headers = [
  'gimpmodule.h',
  'gimpmoduledb.h',
  'gimpmoduletypes.h',
]

libgimpmodule_cflags = [
  '-DG_LOG_DOMAIN="LibGimpModule"',
  '-DGIMP_MODULE_COMPILATION',
]

libgimpmodule_lflags = [
  libgimpbase,
  libgimpconfig,
]

if platform_win32
  # libgimpmodule_lflags += ['-export-symbols', 'gimpmodule.def']
endif


libgimpmodule = library('gimpmodule-' + api_version,
  libgimpmodule_sources,
  include_directories: rootInclude,
  dependencies: [
    gio, glib, gmodule,
  ],
  c_args:     [ libgimp_cflags, libgimpmodule_cflags, ],
  link_with:  [ libgimp_lflags, libgimpmodule_lflags, ],
  install: true,
  version: so_version,
)

install_headers(
  libgimpmodule_headers,
  subdir: join_paths(gimp_api_name, 'libgimpmodule'),
)
