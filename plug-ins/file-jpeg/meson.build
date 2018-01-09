# TODO file-jpeg.rc.o

file_jpeg = executable('file-jpeg',
  [
    'jpeg-icc.c',
    'jpeg-load.c',
    'jpeg-quality.c',
    'jpeg-save.c',
    'jpeg-settings.c',
    'jpeg.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, libjpeg, lcms, gexiv2,
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
