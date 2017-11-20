# TODO file-ico.rc.o

file_ico = executable('file-ico',
  [
    'ico-dialog.c',
    'ico-load.c',
    'ico-save.c',
    'ico.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl,
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
