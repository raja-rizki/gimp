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

if platform_osx
  app_cflags += '-xobjective-c'
  #app_lflags += ['-framework', 'Cocoa']
endif

if platform_win32
  # app_lflags += [ '-mwindows', '-mexchndl', ]
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
  gimpdbusservice_gen,
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
  libappconfig,
  libappcore,
  libappfile,
  libappgegl,
  libappinternalprocs,
  libapplayermodes,
  libapplayermodeslegacy,
  libappoperations,
  libapppaint,
  libapppdb,
  libappplugin,
  libapptext,
  libappvectors,
  libappxcf,
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
  libgimpmath,
  libgimpmodule,
  libgimpthumb,
]

app_gui_links = [
  libappactions,
  libappdialogs,
  libappdisplay,
  libappgui,
  libappmenus,
  libapppropgui,
  libapptools,
  libappwidgets,
  libgimpwidgets,
]

app_deps = [
  gio, gtk2, pangocairo, pangoft2, gegl, lcms, gexiv2,
]

# Executables

gimpconsole_exe = executable('gimp-console-'+app_version,
  libapp_sources + [ 'main.c' ],
  c_args: app_cflags + [ '-DGIMP_CONSOLE_COMPILATION', ],
  include_directories: [ rootInclude, ],
  dependencies: app_deps,
  link_with: app_links,
  install: true,
)

gimpmain_exe = executable('gimp-'+app_version,
  libapp_sources + [ 'main.c' ],
  c_args: app_cflags + [ ],
  include_directories: [ rootInclude, ],
  dependencies: app_deps,
  link_with: app_links + app_gui_links,
  install: true,
)
