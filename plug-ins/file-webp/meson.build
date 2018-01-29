if webp.found()

# TODO file-webp.rc.o

file_webp = executable('file-webp',
  [
    'file-webp-dialog.c',
    'file-webp-load.c',
    'file-webp-save.c',
    'file-webp.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gexiv2, webp,
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
