
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


libgimpmath_cflags = [
  '-DG_LOG_DOMAIN="LibGimpMath"',
  '-DGIMP_MATH_COMPILATION',
]

libgimpmath_lflags = [
  libgimpbase,
]

if os_win32
  libgimpmath_lflags += ['-export-symbols', 'gimpmath.def']
endif


libgimpmath = library('gimpmath-' + api_version,
  libgimpmath_sources,
  include_directories: rootInclude,
  dependencies: [
    glib, gobject, math,
  ],
  c_args:     [ libgimp_cflags, libgimpmath_cflags, ],
  link_with:  [ libgimp_lflags, libgimpmath_lflags, ],
)

install_headers(
  libgimpmath_headers,
  install_dir: join_paths(gimp_api_name, 'libgimpmath'),
)
