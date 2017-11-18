
plugin_selection_to_path_sources = [
  'curve.c',
  'edge.c',
  'fit.c',
  'math.c',
  'pxl-outline.c',
  'selection-to-path-dialog.c',
  'selection-to-path.c',
  'spline.c',
  'vector.c',
]
plugin_selection_to_path_link = [
  libgimp,
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
  libgimpmath,
  libgimpui,
  libgimpwidgets,
]
plugin_selection_to_path_deps = [
  gegl, gtk2,
]
plugin_selection_to_path_lflags = []
if os_win32
  plugin_selection_to_path_lflags += '-mwindows'
else
  plugin_selection_to_path_deps += math
endif


selection_to_path = executable('selection-to-path',
  plugin_selection_to_path_sources,
  include_directories: [ rootInclude, ],
  link_with:    plugin_selection_to_path_link,
  link_args:    plugin_selection_to_path_lflags,
  dependencies: plugin_selection_to_path_deps,
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)
