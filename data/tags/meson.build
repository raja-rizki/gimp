
xmlfilename = 'gimp-tags-default.xml'

gimp_tags_default = custom_target(xmlfilename,
  input : [ xmlfilename+'.in', ],
  output: [ xmlfilename, ],

  command: [
    intltool_merge,
    '--xml-style',
    '--utf8',
    '--cache='+join_paths('@OUTDIR@', 'intltool-merge-cache'),
    potags_dir,
    '@INPUT@',
    '@OUTPUT@',
  ],
  install: true,
  install_dir: join_paths(datadir, 'tags'),
)


custom_target('validate-tags',
  input : [ gimp_tags_default, ],
  output: [ 'validate-tags' ],
  command: [
    xmllint,
    '--noout',
    '--path', join_paths(meson.source_root(), meson.current_source_dir()),
    '--valid', '@INPUT@',
  ],
  build_always: true,
  build_by_default: false,
)
