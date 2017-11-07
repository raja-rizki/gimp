


if os_win32
  gimp_debug_resume = executable('gimp-debug-resume', 'gimp-debug-resume.c')
endif



tools_cflags = [
  '-DBINDIR="'+ get_option('bindir') +'"',
  '-DCC="'+ cc.get_id() +'"',
  '-DDATADIR="'+ datadir +'"',
  '-DDATAROOTDIR="'+ datadir +'"',
  '-DEXEC_PREFIX="'+ prefix +'"',
  '-DGIMP_APP_VERSION="'+ app_version +'"',
  '-DGIMP_PLUGIN_VERSION="'+ plugin_version +'"',
  '-DGIMPDATADIR="'+ datadir +'"',
  '-DGIMPDIR="'+ gimpdir +'"',
  '-DGIMPPLUGINDIR="'+ plugindir +'"',
  '-DINFODIR="'+ get_option('infodir') +'"',
  '-DLIBDIR="'+ get_option('libdir') +'"',
  '-DLIBEXECDIR="'+ get_option('libexecdir') +'"',
  '-DLOCALEDIR="'+ localedir +'"',
  '-DLOCALSTATEDIR="'+ get_option('localstatedir') +'"',
  '-DMANDIR="'+ get_option('mandir') +'"',
  '-DPREFIX="'+ prefix +'"',
  '-DSBINDIR="'+ get_option('sbindir') +'"',
  '-DSHAREDSTATEDIR="'+ get_option('sharedstatedir') +'"',
  '-DSYSCONFDIR="'+ sysconfdir +'"',
]




gimptool = executable('gimptool-2.0',
  'gimptool.c',

  include_directories: rootInclude,
  dependencies: [
    gtk2,
  ],
  link_with: [
    libgimpbase,
  ],
  c_args: tools_cflags,
  install: true,
)


executable('kernelgen',
  'kernelgen.c',
  include_directories: rootInclude,
  install: false,
)
executable('test-clipboard',
  'test-clipboard.c',
  include_directories: rootInclude,
  dependencies: [
    gtk2,
  ],
  install: false,
)

if have_vector_icons
  executable('invert-svg',
    'invert-svg.c',
    dependencies: gio,
  )
endif
