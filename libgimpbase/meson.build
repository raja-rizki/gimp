
global_cflags = []
global_lflags = []

global_cflags += [
  '-DPREFIX="'+ prefix + '"',
  '-DGIMPDIR="'+ gimpdir + '"',
  '-DDATADIR="'+ datadir + '"',
  '-DLOCALEDIR="'+ localedir + '"',
  '-DPLUGINDIR="'+ plugindir + '"',
  '-DSYSCONFDIR="'+ sysconfdir + '"',
  '-DGIMP_PACKAGE="'+ gettext_package + '"',
  '-DGIMP_DATA_VERSION="'+ data_version + '"',
  '-DGIMP_USER_VERSION="'+ user_version + '"',
  '-DGIMP_SYSCONF_VERSION="'+ sysconf_version + '"',
  '-DGIMP_PLUGIN_VERSION="'+ plugin_version + '"',
]


if platform_win32
  global_cflags += '-no-undefined'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  global_lflags += '-lole32'
  # global_lflags += ['-export-symbols', 'gimpbase.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpBase' + '"',
  '-DGIMP_BASE_COMPILATION',
]

libgimpbase_sources = [
  'gimpbase-private.c',
  'gimpbaseenums.c',
  'gimpbasetypes.c',
  'gimpchecks.c',
  'gimpcompatenums.c',
  'gimpcpuaccel.c',
  'gimpdatafiles.c',
  'gimpenv.c',
  'gimpmemsize.c',
  'gimpmetadata.c',
  'gimpparasite.c',
  'gimpparasiteio.c',
  'gimpprotocol.c',
  'gimprectangle.c',
  'gimpreloc.c',
  'gimpsignal.c',
  'gimpunit.c',
  'gimputils.c',
  'gimpvaluearray.c',
  'gimpwire.c',
]

# TODO add auto-generation targets for those files
libgimpbase_sources += [
  'gimpbaseenums.c',
  'gimpcompatenums.c',
]

libgimpbase_headers = [
  'gimpbase.h',
  'gimpbaseenums.h',
  'gimpbasetypes.h',
  'gimpcpuaccel.h',
  'gimplimits.h',
  'gimpparam.h',
  'gimpversion.h',
  'gimpchecks.h',
  'gimpdatafiles.h',
  'gimpenv.h',
  'gimpmemsize.h',
  'gimpmetadata.h',
  'gimpparasite.h',
  'gimpparasiteio.h',
  'gimprectangle.h',
  'gimpsignal.h',
  'gimpunit.h',
  'gimputils.h',
  'gimpvaluearray.h',
]




libgimpbase = library('gimpbase-' + api_version,
  libgimpbase_sources,
  include_directories: rootInclude,
  dependencies: [
    gio, gexiv2, math,
  ],
  c_args: global_cflags,
  link_with: global_lflags,
)

install_headers(
  libgimpbase_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpbase'),
)


# test programs, not to be built by default and never installed
test_cpu_accel = executable('test-cpu-accel',
  'test-cpu-accel.c',
  include_directories: rootInclude,
  dependencies: [
    glib,
  ],
  c_args: global_cflags,
  link_with: libgimpbase,
  install: false,
)
