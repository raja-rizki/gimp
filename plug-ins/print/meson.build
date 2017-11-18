plugin_print_sources = [
  'print-draw-page.c',
  'print-page-layout.c',
  'print-page-setup.c',
  'print-preview.c',
  'print-settings.c',
  'print-utils.c',
  'print.c',
]
# TODO print.rc.o
print = executable('print',
  plugin_print_sources,
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl,
    x11, xmu, xext, xfixes,
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
