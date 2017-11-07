
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
  # global_lflags += ['-export-symbols', 'gimpconfig.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpConfig' + '"',
  '-DGIMP_CONFIG_COMPILATION',
]




libgimpconfig_sources = [
  'gimpcolorconfig.c',
  'gimpconfig-deserialize.c',
  'gimpconfig-error.c',
  'gimpconfig-iface.c',
  'gimpconfig-path.c',
  'gimpconfig-serialize.c',
  'gimpconfig-utils.c',
  'gimpconfigenums.c',
  'gimpconfigwriter.c',
  'gimpscanner.c',
]

libgimpconfig_sources += [
  'gimpconfigenums.c',
]


libgimpconfig_headers = [
  'gimpcolorconfig.h',
  'gimpconfig-deserialize.h',
  'gimpconfig-error.h',
  'gimpconfig-iface.h',
  'gimpconfig-params.h',
  'gimpconfig-path.h',
  'gimpconfig-serialize.h',
  'gimpconfig-utils.h',
  'gimpconfig.h',
  'gimpconfigenums.h',
  'gimpconfigtypes.h',
  'gimpconfigwriter.h',
  'gimpscanner.h',
]


libgimpconfig = library('gimpconfig-'+ api_version,
  libgimpconfig_sources,
  include_directories: rootInclude,
  dependencies: [
    cairo, gdk_pixbuf, gegl, gio, gio_specific,
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, libgimpcolor, libgimpmath, ],
)

install_headers(
  libgimpconfig_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpconfig'),
)
