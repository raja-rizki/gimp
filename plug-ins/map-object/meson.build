# TODO map-object.rc.o

map_object = executable('map-object',
  [
    'arcball.c',
    'map-object-apply.c',
    'map-object-image.c',
    'map-object-main.c',
    'map-object-preview.c',
    'map-object-shade.c',
    'map-object-stock.c',
    'map-object-ui.c',
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
