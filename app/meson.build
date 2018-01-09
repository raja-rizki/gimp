rootAppInclude = include_directories('.')

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

app_mkenums_custom_target_command = [
  gimp_mkenums,
  '--fhead','#include "config.h"\n'
          + '#include <gio/gio.h>\n'
          + '#include "libgimpbase/gimpbase.h"\n'
          + '#include "core/core-enums.h"\n'
          + '#include "@INPUT@"\n'
          + '#include "gimp-intl.h"\n',
  gimp_mkenums_custom_target_commonargs,
]

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
app_lflags = [
]
app_cflags = [
  '-DCC_VERSION="' + cc.version() + '"',
  '-DG_LOG_DOMAIN="Gimp"',
  '-DGIMP_APP_GLUE_COMPILATION',
  '-DGIMP_USER_VERSION="'+ user_version +'"',
  '-DGIMPDIR="'+ gimpdir + '"',
]

if platform_win32
  app_cflags += '-no-undefined'
  app_lflags += '-lgdi32'
endif

if platform_osx
  app_cflags += '-xobjective-c'
  app_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  app_lflags += [ '-mwindows', '-mexchndl', ]
  # app_lflags += ['-export-symbols', 'gimpwidgets.def']
endif

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
  c_args: app_cflags,
  dependencies: [
    gegl, gdk_pixbuf, gtk2,
  ],
  link_with: app_lflags,
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
app_deps = [
  gio, gtk2, pangocairo, gegl, lcms, gexiv2,
]

# Executables

gimpconsole_exe = executable('gimp-console-'+app_version,
  'main.c',
  c_args: app_cflags + [ '-DGIMP_CONSOLE_COMPILATION', ],
  include_directories: [ rootInclude, ],
  dependencies: app_deps,
  link_with: app_links,
  install: true,
)

gimpmain_exe = executable('gimp-'+app_version,
  'main.c',
  c_args: app_cflags + [ ],
  include_directories: [ rootInclude, ],
  dependencies: app_deps,
  link_with: app_links,
  install: true,
)
