# TODO fractal-explorer.rc.o

fractal_explorer = executable('fractal-explorer',
  [
    'fractal-explorer-dialogs.c',
    'fractal-explorer.c',
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
