
if platform_win32
  gimp_debug_resume = executable('gimp-debug-resume', 'gimp-debug-resume.c')
endif


gimptool = executable('gimptool-2.0',
  'gimptool.c',

  include_directories: rootInclude,
  dependencies: [
    gtk2,
  ],
  link_with: [
    libgimpbase,
  ],
  install: true,
)


executable('kernelgen',
  'kernelgen.c',
  include_directories: rootInclude,
  install: false,
)
executable('test-clipboard',
  'test-clipboard.c',
  include_directories: rootInclude,
  dependencies: [
    gtk2,
  ],
  install: false,
)

if have_vector_icons
  invert_svg_exe = executable('invert-svg',
    'invert-svg.c',
    dependencies: gio,
  )
  invert_svg = generator(
    invert_svg_exe,
    output: '@BASENAME@',
    arguments: [ '@INPUT@', '@OUTPUT@' ],
  )
endif
