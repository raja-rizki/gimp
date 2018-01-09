subdir('doc')
subdir('plug-ins')

plugin_pygimp_sources = [
  'gimpmodule.c',
  'pygimp-display.c',
  'pygimp-drawable.c',
  'pygimp-image.c',
  'pygimp-item.c',
  'pygimp-parasite.c',
  'pygimp-pdb.c',
  'pygimp-tile.c',
  'pygimp-vectors.c',
]
# TODO pygimp.rc.o
pygimp = executable('pygimp',
  plugin_pygimp_sources,
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






path_separator = platform_win32 ? ';' : ':'

custom_target('pygimp.env',
  input : [],
  output: [ 'pygimp.env' ],
  command: [
    'echo', path_separator + ' PYTHONPATH=${gimp_plug_in_dir}/python'
  ],
  capture: true,
  install: true,
  install_dir: join_paths(gimpplugindir, 'environ'),
)
custom_target('pygimp.interp',
  input : [],
  output: [ 'pygimp.interp' ],
  command: [
    'echo', 'python=' + pythonmod.find_python().path()
    + '\n'+ '/usr/bin/python=' + pythonmod.find_python().path()
    + '\n'+ ':Python:E::py::python:'
  ],
  capture: true,
  install: true,
  install_dir: join_paths(gimpplugindir, 'interpreters'),
)
