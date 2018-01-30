if have_scriptfu

scriptfu_incdir = include_directories('.')

subdir('tinyscheme')
subdir('ftx')
subdir('scripts')

plugin_scriptfu_sources = [
  'scheme-wrapper.c',
  'script-fu-console.c',
  'script-fu-eval.c',
  'script-fu-interface.c',
  'script-fu-regex.c',
  'script-fu-script.c',
  'script-fu-scripts.c',
  'script-fu-server.c',
  'script-fu-text-console.c',
  'script-fu-utils.c',
  'script-fu.c',
]

winsock = platform_win32 ? cc.find_library('ws2_32') : []

scriptfu = executable('script-fu',
  plugin_scriptfu_sources,
  include_directories: [ rootInclude, ],
  dependencies: [
    gegl, gtk2, math, winsock,
  ],
  c_args: [
    '-DSTANDALONE=0',
    '-DUSE_INTERFACE=1',
    '-DUSE_STRLWR=0',
  ],
  link_whole: [
    scriptfu_tinyscheme,
    scriptfu_ftx,
  ],
  link_with: [
    libgimp,
    libgimpbase,
    libgimpcolor,
    libgimpconfig,
    libgimpmath,
    libgimpui,
    libgimpwidgets,
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)

endif
