# TODO file-tiff.rc.o

file_tiff = executable('file-tiff',
  [
    'file-tiff-io.c',
    'file-tiff-save.c',
    'file-tiff.c',
    'file-tiff-load.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gexiv2, webp, libtiff,
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
