# TODO gradient-flare.rc.o

gradient_flare = executable('gradient-flare',
  [
    'gradient-flare.c',
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
  c_args: [
    '-DDATADIR="' + gimpdatadir + '"',
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)

install_data([
    join_paths('flares', 'Bright_Star'),
    join_paths('flares', 'Classic'),
    join_paths('flares', 'Default'),
    join_paths('flares', 'Distant_Sun'),
    join_paths('flares', 'GFlare_101'),
    join_paths('flares', 'GFlare_102'),
    join_paths('flares', 'Hidden_Planet'),
  ],
  install_dir: join_paths(gimpdatadir, 'gflare'),
)
