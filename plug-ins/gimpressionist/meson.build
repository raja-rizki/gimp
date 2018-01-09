# TODO gimpressionist.rc.o

gimpressionist = executable('gimpressionist',
  [
    'brush.c',
    'color.c',
    'general.c',
    'gimp.c',
    'gimpressionist.c',
    'globals.c',
    'orientation.c',
    'orientmap.c',
    'paper.c',
    'placement.c',
    'plasma.c',
    'ppmtool.c',
    'presets.c',
    'preview.c',
    'repaint.c',
    'size.c',
    'sizemap.c',
    'utils.c',
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
    '-DDEFAULTPATH="' + join_paths('~/',  gimpdir,    'gimpressionist')
                + ':' + join_paths(prefix,gimpdatadir,'gimpressionist')
                + '"',
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)
