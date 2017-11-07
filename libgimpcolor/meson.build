
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
  # global_lflags += '-lole32'
  # global_lflags += ['-export-symbols', 'gimpbase.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpColor' + '"',
  '-DGIMP_COLOR_COMPILATION',
]




libgimpcolor_sources = [
  'gimpadaptivesupersample.c',
  'gimpbilinear.c',
  'gimpcairo.c',
  'gimpcmyk.c',
  'gimpcolormanaged.c',
  'gimpcolorprofile.c',
  'gimpcolorspace.c',
  'gimpcolortransform.c',
  'gimphsl.c',
  'gimphsv.c',
  'gimppixbuf.c',
  'gimprgb-parse.c',
  'gimprgb.c',
]

libgimpcolor_headers = [
  'gimpcolor.h',
  'gimpcolortypes.h',
  'gimpadaptivesupersample.h',
  'gimpbilinear.h',
  'gimpcairo.h',
  'gimpcmyk.h',
  'gimpcolormanaged.h',
  'gimpcolorprofile.h',
  'gimpcolorspace.h',
  'gimpcolortransform.h',
  'gimphsl.h',
  'gimphsv.h',
  'gimppixbuf.h',
  'gimprgb.h',
]


libgimpcolor = library('gimpcolor-'+ api_version,
  libgimpcolor_sources,
  include_directories: rootInclude,
  dependencies: [
    cairo, gdk_pixbuf, gegl, lcms, math,
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, ],
)

install_headers(
  libgimpcolor_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpcolor'),
)


# test programs, not to be built by default and never installed
test_color_parser = executable('test-color-parser',
  'test-color-parser.c',
  include_directories: rootInclude,
  dependencies: [
    babl, cairo, gdk_pixbuf, gegl, glib,
  ],
  c_args: global_cflags,
  link_with: libgimpcolor,
  install: false,
)
