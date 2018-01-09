# TODO gradient-flare.rc.o
subdir('flares')

gradient_flare = executable('gradient-flare',
  [
    'gradient-flare.c',
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
  c_args: [
    '-DDATADIR="' + join_paths(prefix, gimpdatadir) + '"',
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)
