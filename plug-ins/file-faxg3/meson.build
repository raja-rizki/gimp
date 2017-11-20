# TODO file-faxg3.rc.o

file_faxg3 = executable('file-faxg3',
  [
    'faxg3.c',
    'g3.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gdk_pixbuf, cairo,
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
