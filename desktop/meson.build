sizes = [
  '16',
  '22',
  '24',
  '32',
  '48',
  '64',
  '256',
]

foreach size : sizes
  sizedir = size+'x'+size
  install_data(join_paths(sizedir, 'gimp.png'),
    install_dir: join_paths(
      get_option('datadir'), 'icons', 'hicolor', sizedir, 'apps'
    )
  )
endforeach

desktopfilename = 'gimp.desktop'

desktop_conf = configuration_data()
desktop_conf.set('GIMP_APP_VERSION', app_version)
desktop_conf.set('GIMP_COMMAND', gimp_command)
desktop_conf.set('GIMP_VERSION', user_version)
desktop_conf.set('MIME_TYPES', ';'.join(MIMEtypes))

desktopfilein = configure_file(
  input : desktopfilename+'.in.in',
  output: desktopfilename+'.in',
  configuration: desktop_conf,
)

desktopfile = custom_target(desktopfilename,
  input : [ desktopfilein, ],
  output: [ desktopfilename, ],

  command: [
    intltool_merge,
    '--desktop-style',
    '--utf8',
    '--cache='+join_paths('@OUTDIR@', 'intltool-merge-cache'),
    po_dir,
    '@INPUT@',
    '@OUTPUT@',
  ],
  install: true,
  install_dir: join_paths(get_option('datadir'), 'applications'),
)


custom_target('validate-desktop',
  input : [ desktopfile, ],
  output: [ 'validate-desktop' ],
  command: [
    desktop_validate, '@INPUT@',
  ],
  build_always: true,
  build_by_default: false,
)
