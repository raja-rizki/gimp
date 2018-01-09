
if os_win32
  gimp_debug_resume = executable('gimp-debug-resume', 'gimp-debug-resume.c')
endif



tools_cflags = [
  '-DGIMP_APP_VERSION='    +'"'+ app_version                                    +'"',
  '-DGIMP_PLUGIN_VERSION=' +'"'+ api_version                                    +'"',

  '-DCC='                  +'"'+ cc.get_id()                                    +'"',

  '-DPREFIX='              +'"'+ prefix                                         +'"',
  '-DEXEC_PREFIX='         +'"'+ prefix                                         +'"',
  '-DBINDIR='              +'"'+ join_paths(prefix, get_option('bindir'))       +'"',
  '-DDATADIR='             +'"'+ join_paths(prefix, get_option('datadir'))      +'"',
  '-DDATAROOTDIR='         +'"'+ join_paths(prefix, get_option('datadir'))      +'"',
  '-DGIMPDATADIR='         +'"'+ join_paths(prefix, gimpdatadir)                +'"',
  '-DGIMPDIR='             +'"'+ gimpdir                                        +'"',
  '-DGIMPPLUGINDIR='       +'"'+ join_paths(prefix, gimpplugindir)              +'"',
  '-DINFODIR='             +'"'+ join_paths(prefix, get_option('infodir'))      +'"',
  '-DLIBDIR='              +'"'+ join_paths(prefix, get_option('libdir'))       +'"',
  '-DLIBEXECDIR='          +'"'+ join_paths(prefix, get_option('libexecdir'))   +'"',
  '-DLOCALEDIR='           +'"'+ join_paths(prefix, localedir)                  +'"',
  '-DMANDIR='              +'"'+ join_paths(prefix, get_option('mandir'))       +'"',
  '-DSBINDIR='             +'"'+ join_paths(prefix, get_option('sbindir'))      +'"',
  '-DLOCALSTATEDIR='       +'"'+ get_option('localstatedir')                    +'"',
  '-DSHAREDSTATEDIR='      +'"'+ get_option('sharedstatedir')                   +'"', # HUH ? /usr/com
  '-DSYSCONFDIR='          +'"'+ get_option('sysconfdir')                       +'"',
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
  invert_svg_exe = executable('invert-svg',
    'invert-svg.c',
    dependencies: gio,
  )
  invert_svg = generator(
    invert_svg_exe,
    output: '@BASENAME@',
    arguments: [ '@INPUT@', '@OUTPUT@' ],
  )
endif
