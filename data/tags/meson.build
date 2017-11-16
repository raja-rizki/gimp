
intltool_merge = find_program('intltool-merge')

xmlfilename = 'gimp-tags-default.xml'

gimp_tags_default = custom_target(xmlfilename,
  input : xmlfilename+'.in',
  output: xmlfilename,

  command: [
    intltool_merge,
    '--xml-style',
    '--utf8',
    '--cache=intltool-merge-cache',
    potags_dir,
    '@INPUT@',
    '@OUTPUT@',
  ],
  install: true,
  install_dir: join_paths(datadir, 'tags'),
)


custom_target('validate',
  input : gimp_tags_default,
  output: [ 'validate' ],
  command: [
    xmllint,
    '--noout',
    '--path', join_paths(meson.source_root(), meson.current_source_dir()),
    '--valid', '@INPUT@',
  ],
  build_always: true,
  build_by_default: false,
)
