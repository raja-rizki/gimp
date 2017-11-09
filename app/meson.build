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
# Those subdirs need to link againts the first ones
# subdir('config')
# subdir('tests')
