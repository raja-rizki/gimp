# TODO ifs-compose.rc.o

ifs_compose = executable('if-compose',
  [
    'ifs-compose-storage.c',
    'ifs-compose-utils.c',
    'ifs-compose.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, math,
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
