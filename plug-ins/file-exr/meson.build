if openexr.found()

# TODO file-exr.rc.o

file_exr = executable('file-exr',
  [
    'file-exr.c',
    'openexr-wrapper.cc',
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, openexr, lcms,
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

endif
