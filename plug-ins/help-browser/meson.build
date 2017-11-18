# TODO help-browser.rc.o

help_browser = executable('help-browser',
  [
    'dialog.c',
    'gimpthrobber.c',
    'gimpthrobberaction.c',
    'help-browser.c',
    'uri.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gio, webkit,
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
