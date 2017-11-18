# TODO metadata-editor.rc.o
# TODO metadata-viewer.rc.o

metadata_editor = executable('metadata-editor',
  [
    'metadata-editor.c',
    'metadata-impexp.c',
    'metadata-xml.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gexiv2,
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

metadata_viewer = executable('metadata-viewer',
  [
    'metadata-viewer.c',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, gexiv2,
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
