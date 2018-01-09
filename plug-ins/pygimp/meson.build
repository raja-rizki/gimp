subdir('doc')
subdir('plug-ins')


#
# .defs.c:
# 	(cd $(srcdir) \
# 	 && $(PYGTK_CODEGEN) \
# 	    --override $*.override \
# 	    --register $(PYGTK_DEFSDIR)/gdk-types.defs \
# 	    --register $(PYGTK_DEFSDIR)/gtk-types.defs \
# 	    --register gimp-types.defs \
# 	    --register gimpcolor-types.defs \
# 	    --register gimpenums-types.defs \
# 	    --prefix $* $*.defs) > gen-$*.c \
# 	 && cp gen-$*.c $*.c \
# 	 && rm -f gen-$*.c



python_so_libs = [
  [ 'gimp', [
      'gimpmodule.c',
      'pygimp-display.c',
      'pygimp-drawable.c',
      'pygimp-image.c',
      'pygimp-item.c',
      'pygimp-parasite.c',
      'pygimp-pdb.c',
      'pygimp-tile.c',
      'pygimp-vectors.c',
    ],
  ],
  [ '_gimpenums', [ 'gimpenumsmodule.c',                    ], ],
  [ '_gimpui',    [ 'gimpuimodule.c',    'gimpui.c',        ], ],
  [ 'gimpcolor',  [ 'gimpcolormodule.c', 'pygimp-colors.c', ], ],
  [ 'gimpthumb',  [ 'gimpthumbmodule.c', 'gimpthumb.c',     ], ],
]

foreach pylib : python_so_libs
  shared_library(pylib[0],
    pylib[1],
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
    install_dir: join_paths(gimpplugindir, 'python'),
  )
endforeach

install_data([
  'gimpenums.py',
  'gimpfu.py',
  'gimpplugin.py',
  'gimpshelf.py',
  'gimpui.py',
  'pygimp-logo.png',
  ],
  install_dir: join_paths(gimpplugindir, 'python'),
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
