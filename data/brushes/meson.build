brushes = run_command('find',
  meson.current_source_dir(),
  '-maxdepth', '1',
  '-mindepth', '1',
  '-type', 'd',
  '-printf', '%f\n'
).stdout().strip().split('\n')

foreach brush : brushes
  files = run_command('find',
    join_paths(meson.current_source_dir(), brush),
    '-type', 'f',
    '(',
    '-name', '*.gbr',
    '-o',
    '-name', '*.gih',
    '-o',
    '-name', '*.vbr',
    ')',
    '-printf', brush + '/%f\n'
  ).stdout().strip().split('\n')


  install_data(files,
    install_dir: join_paths(datadir, 'brushes', brush)
  )
endforeach
