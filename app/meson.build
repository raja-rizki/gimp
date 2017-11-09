rootAppInclude = include_directories('.')

subdir('actions')
subdir('core')
subdir('dialogs')
subdir('display')
subdir('file')
subdir('gegl')
subdir('gui')
subdir('menus')
subdir('operations')
subdir('paint')
subdir('pdb')
subdir('plug-in')
subdir('propgui')
subdir('text')
subdir('tools')
subdir('vectors')
subdir('widgets')
subdir('xcf')


app_debug_files = files(
  'gimp-debug.c',
  'gimp-log.c',
)

# Top-level library
global_cflags = []
global_lflags = []

global_cflags += [
  '-DGIMPDIR="'+ gimpdir + '"',
  '-DGIMP_USER_VERSION="'+ user_version +'"',
  '-DG_LOG_DOMAIN="Gimp"',
  '-DGIMP_APP_GLUE_COMPILATION',
  '-DCC_VERSION="' + cc.version() + '"',
]

if platform_win32
  global_cflags += '-no-undefined'
  global_lflags += '-lgdi32'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  global_lflags += [ '-mwindows', '-mexchndl', ]
  # global_lflags += ['-export-symbols', 'gimpwidgets.def']
endif


gitversion_h1 = vcs_tag(
  input : 'git-version.h.in',
  output: 'git-version.h.in.1',
  command: [ 'git', 'describe', '--always', ],
  replace_string: '@GIMP_GIT_VERSION@',
  fallback: '',
)
gitversion_h2 = vcs_tag(
  input : gitversion_h1,
  output: 'git-version.h.in.2',
  command: [ 'git', 'rev-parse', '--short', 'HEAD', ],
  replace_string: '@GIMP_GIT_VERSION_ABBREV@',
  fallback: '',
)
gitversion_h = vcs_tag(
  input : gitversion_h2,
  output: 'git-version.h',
  command: [ 'git', 'log', '-n1', '--date=format:%Y', '--pretty=%cd', ],
  replace_string: '@GIMP_GIT_LAST_COMMIT_YEAR@',
  fallback: '',
)

libapp_sources = [
  'app.c',
  'errors.c',
  'gimp-debug.c',
  'gimp-log.c',
  'language.c',
  'sanity.c',
  'signals.c',
  'tests.c',
  'unique.c',
  'version.c',
  gitversion_h,
]

libapp = static_library('app',
  libapp_sources,
  include_directories: [ rootInclude, rootAppInclude, configInclude, ],
  c_args: global_cflags,
  dependencies: [
    gegl, gdk_pixbuf, gtk2,
  ],
  link_with: global_lflags,


)




# Those subdirs need to link againts the first ones
subdir('config')
subdir('tests')

app_links = [
  libapp,
  libappactions,
  libappconfig,
  libappcore,
  libappdialogs,
  libappdialogs,
  libappdisplay,
  libappfile,
  libappgegl,
  libappgui,
  libappinternalprocs,
  libapplayermodes,
  libapplayermodeslegacy,
  libappmenus,
  libappoperations,
  libapppaint,
  libapppdb,
  libappplugin,
  libapppropgui,
  libapptext,
  libapptools,
  libappvectors,
  libappwidgets,
  libappxcf,
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
  libgimpmath,
  libgimpmodule,
  libgimpthumb,
  libgimpwidgets,
]


# Executables

# xcf/libappxcf.a						\
# pdb/libappinternal-procs.a				\
# pdb/libapppdb.a						\
# plug-in/libappplug-in.a					\
# vectors/libappvectors.a					\
# core/libappcore.a					\
# file/libappfile.a					\
# text/libapptext.a					\
# paint/libapppaint.a					\
# operations/libappoperations.a				\
# operations/layer-modes/libapplayermodes.a		\
# operations/layer-modes-legacy/libapplayermodeslegacy.a	\
# gegl/libappgegl.a					\
# config/libappconfig.a					\
# $(libgimpconfig)					\
# $(libgimpmath)						\
# $(libgimpthumb)						\
# $(libgimpcolor)						\
# $(libgimpmodule)					\
# $(libgimpbase)						\
