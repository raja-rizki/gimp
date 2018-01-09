# TODO flame.rc.o

flame = executable('flame',
  [
    'cmap.c',
    'flame.c',
    'libifs.c',
    'rect.c',
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
