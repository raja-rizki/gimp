
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
  '-DG_LOG_DOMAIN="'+ 'LibGimpThumb' + '"',
  '-DGIMP_THUMB_COMPILATION',
]



libgimpthumb_sources = [
  'gimpthumb-error.c',
  'gimpthumb-utils.c',
  'gimpthumbnail.c',
]

# TODO mkenums
libgimpthumb_sources += [
  'gimpthumb-enums.c',
]


libgimpthumb_headers = [
  'gimpthumb-enums.h',
  'gimpthumb-error.h',
  'gimpthumb-types.h',
  'gimpthumb-utils.h',
  'gimpthumb.h',
  'gimpthumbnail.h',
]


libgimpthumb = library('gimpthumb-'+ api_version,
  libgimpthumb_sources,
  include_directories: rootInclude,
  dependencies: [
    gdk_pixbuf, glib, gio, gobject,
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, ],
)

install_headers(
  libgimpthumb_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpthumb'),
)


# test programs, not to be built by default and never installed
gimp_thumbnail_list = executable('gimp-thumbnail-list',
  'gimp-thumbnail-list.c',
  include_directories: rootInclude,
  dependencies: [
    gdk_pixbuf, glib, gio, gobject,
  ],
  c_args: global_cflags,
  link_with: libgimpthumb,
  install: false,
)
