# TODO file-raw.rc.o

file_raw_exes = [
  'file-darktable',
  'file-raw-placeholder',
  'file-rawtherapee',
]

foreach file_raw_exename : file_raw_exes
  file_raw = executable(file_raw_exename,
    [
      file_raw_exename +'.c',
      'file-raw-utils.c',
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
endforeach

install_data([
    'file-darktable-export-on-exit.lua',
    'file-darktable-get-size.lua',
  ],
  install_dir: join_paths(prefix, gimpdatadir, 'file-raw'),
)
