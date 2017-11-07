libappconfig_sources = [
  'gimpconfig-dump.c',
  'gimpconfig-file.c',
  'gimpconfig-utils.c',
  'gimpcoreconfig.c',
  'gimpdialogconfig.c',
  'gimpdisplayconfig.c',
  'gimpdisplayoptions.c',
  'gimpgeglconfig.c',
  'gimpguiconfig.c',
  'gimplangrc.c',
  'gimppluginconfig.c',
  'gimprc-deserialize.c',
  'gimprc-serialize.c',
  'gimprc-unknown.c',
  'gimprc.c',
  'gimpxmlparser.c',
]

# TODO mkenums
libappconfig_sources += [
  'config-enums.c',
]


libappconfig = static_library('appconfig',
  libappconfig_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Config"',
    '-DGIMP_APP_VERSION_STRING="'+ app_version +'"',
    '-DDATADIR="'+ datadir +'"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf, gio, gio_specific, gtk2,
  ],
)


executable('test-config',
  'test-config.c',
  include_directories: [ rootInclude, rootAppInclude, ],

  dependencies: [
    gegl, gio, gio_specific,
  ],
  link_with: [
    libgimpbase,
    libgimpconfig,
    libgimpcolor,
    libgimpmath,
    libappconfig,
    libappcore,
  ]


)