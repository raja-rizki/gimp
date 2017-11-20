# TODO file-psd.rc.o

file_psd = executable('file-psd',
  [
    'psd-image-res-load.c',
    'psd-layer-res-load.c',
    'psd-load.c',
    'psd-save.c',
    'psd-thumb-load.c',
    'psd-util.c',
    'psd.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl
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
