# TODO lighting.rc.o
subdir('images')

lighting = executable('lighting',
  [
    'lighting-apply.c',
    'lighting-image.c',
    'lighting-main.c',
    'lighting-preview.c',
    'lighting-shade.c',
    'lighting-stock.c',
    'lighting-ui.c',
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
