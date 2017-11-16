
menu_files = [
  'brush-editor-menu.xml',
  'brushes-menu.xml',
  'buffers-menu.xml',
  'channels-menu.xml',
  'colormap-menu.xml',
  'cursor-info-menu.xml',
  'documents-menu.xml',
  'dynamics-editor-menu.xml',
  'dynamics-menu.xml',
  'error-console-menu.xml',
  'fonts-menu.xml',
  'gradient-editor-menu.xml',
  'gradients-menu.xml',
  'images-menu.xml',
  'layers-menu.xml',
  'mypaint-brushes-menu.xml',
  'palette-editor-menu.xml',
  'palettes-menu.xml',
  'patterns-menu.xml',
  'quick-mask-menu.xml',
  'sample-points-menu.xml',
  'selection-menu.xml',
  'templates-menu.xml',
  'text-editor-toolbar.xml',
  'text-tool-menu.xml',
  'tool-options-menu.xml',
  'tool-preset-editor-menu.xml',
  'tool-presets-menu.xml',
  'undo-menu.xml',
  'vectors-menu.xml',
]

unstable_menu_args = stable ? [] : [ '--stringparam', 'unstable-menus', 'yes' ]

foreach menu_filegen : [ 'dockable-menu.xml', 'image-menu.xml', ]
  menu_files += custom_target(menu_filegen,
    input : [ menu_filegen +'.in', 'menus.xsl', ],
    output: [ menu_filegen ],
    command: [
      xsltproc,
      '--xinclude',
      unstable_menu_args,
      '--output', '@OUTPUT@',
      '@INPUT1@',
      '@INPUT0@',
    ],
    build_always: true,
    build_by_default: false,
  )
endforeach

custom_target('validate_menus',
  input : [ menu_files, ],
  output: [ 'validate_menus', ],
  command: [
    xmllint,
    '--noout',
    '--path', join_paths(meson.source_root(), meson.current_source_dir()),
    '@INPUT@',
  ],
)
