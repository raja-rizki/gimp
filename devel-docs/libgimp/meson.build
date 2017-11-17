# version_file = configure_file

gnome.gtkdoc('libgimp',
  main_sgml: 'libgimp-docs.sgml',
  src_dir: [
    join_paths(meson.source_root(), 'libgimp'),
  ],
  scan_args: [
    '--deprecated-guards="GIMP_DISABLE_DEPRECATED"',
  ],
  scanobjs_args: [
    '--verbose',
  ],
  include_directories: [
    include_directories('../../../'),
  ],
  gobject_typesfile: join_paths(meson.source_root(), meson.current_source_dir(), 'libgimp.types'),

  dependencies: [
    gtk2, glib
  ],
  fixxref_args: [
    '--extra-dir='+join_paths(meson.source_root(), 'libgimpbase/html'),
    '--extra-dir='+join_paths(meson.source_root(), 'libgimpcolor/html'),
    '--extra-dir='+join_paths(meson.source_root(), 'libgimpconfig/html'),
    '--extra-dir='+join_paths(meson.source_root(), 'libgimpmath/html'),
    '--extra-dir='+join_paths(meson.source_root(), 'libgimpwidgets/html'),

    # '--extra-dir='+join_paths(meson.build_root(), 'libgimpbase/html'),
    # '--extra-dir='+join_paths(meson.build_root(), 'libgimpcolor/html'),
    # '--extra-dir='+join_paths(meson.build_root(), 'libgimpconfig/html'),
    # '--extra-dir='+join_paths(meson.build_root(), 'libgimpmath/html'),
    # '--extra-dir='+join_paths(meson.build_root(), 'libgimpwidgets/html'),
  ],
  ignore_headers: [
    'gimptilebackendplugin.h',
    'gimpunit_pdb.h',
    'gimpunitcache.h',
    'libgimp-intl.h',
    'stdplugins-intl.h',
  ],
  content_files: [
    'libgimp-sections.txt',
  ],
  html_args: [
  ],
  mkdb_args: [
    # '--name-space=gimp',
  ],
  install: false,
)
