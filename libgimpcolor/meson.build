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

libgimpcolor_cflags = [
  '-DG_LOG_DOMAIN="LibGimpColor"',
  '-DGIMP_COLOR_COMPILATION',
]
libgimpcolor_lflags = [
  libgimpbase,
]

if os_win32
  libgimpcolor_lflags += '-lole32'
  libgimpcolor_lflags += ['-export-symbols', 'gimpcolor.def']
endif


libgimpcolor = library('gimpcolor-' + api_version,
  libgimpcolor_sources,
  include_directories: rootInclude,
  dependencies: [
    cairo, gdk_pixbuf, gegl, lcms, math,
  ],
  c_args:     [ libgimp_cflags, libgimpcolor_cflags, ],
  link_with:  [ libgimp_lflags, libgimpcolor_lflags, ],
  install: true,
  version: so_version,
)

install_headers(
  libgimpcolor_headers,
  subdir: join_paths(gimp_api_name, 'libgimpcolor'),
)


# Test program, not installed
executable('test-color-parser',
  'test-color-parser.c',
  include_directories: rootInclude,
  dependencies: [
    cairo, gdk_pixbuf, gegl, lcms, math,
    babl,
    # glib,
  ],
  c_args:     [ libgimp_cflags, libgimpcolor_cflags, ],
  link_with:  [ libgimp_lflags, libgimpcolor_lflags, libgimpcolor, ],
  install: false,
)
