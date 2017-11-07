
libappxcf = static_library('appxcf',
  [
    'xcf-load.c',
    'xcf-read.c',
    'xcf-save.c',
    'xcf-seek.c',
    'xcf-utils.c',
    'xcf-write.c',
    'xcf.c',
  ],
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-XCF"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf
  ],
)
