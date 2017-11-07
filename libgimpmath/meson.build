
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
  # global_lflags += ['-export-symbols', 'gimpmath.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpMath' + '"',
  '-DGIMP_MATH_COMPILATION',
]



libgimpmath_sources = [
  'gimpmatrix.c',
  'gimpmd5.c',
  'gimpvector.c',
]

libgimpmath_headers = [
  'gimpmath.h',
  'gimpmathtypes.h',
  'gimpmatrix.h',
  'gimpmd5.h',
  'gimpvector.h',
]


libgimpmath = library('gimpmath-'+ api_version,
  libgimpmath_sources,
  include_directories: rootInclude,
  dependencies: [
    glib, gobject, math,
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, ],
)

install_headers(
  libgimpmath_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpmath'),
)
