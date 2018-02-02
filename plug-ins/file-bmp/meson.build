rc_file = platform_win32 ? windows.compile_resources(
  gimp_plugins_rc,
  args: [

  ],
  include_directories: [

  ],
) : []


file_bmp = executable('file-bmp',
  [
    'bmp-load.c',
    'bmp-save.c',
    'bmp.c',
    rc_file,
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
