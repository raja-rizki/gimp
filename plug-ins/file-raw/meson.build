# TODO file-raw.rc.o

file_raw = executable('file-raw',
  [
    'file-darktable.c',
    'file-raw-placeholder.c',
    'file-raw-utils.c',
    'file-rawtherapee.c',
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
