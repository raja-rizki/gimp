# TODO help.rc.o

help = executable('help',
  [
    'gimp-help-lookup.c',
    'gimphelp.c',
    'gimphelpdomain.c',
    'gimphelpitem.c',
    'gimphelplocale.c',
    'gimphelpprogress.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, cairo, gio, gdk_pixbuf,
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
