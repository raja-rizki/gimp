presets = run_command('find',
  meson.current_source_dir(),
  '-maxdepth', '1',
  '-mindepth', '1',
  '-type', 'd',
  '-printf', '%f\n'
).stdout().strip().split('\n')

foreach preset : presets
  files = run_command('find',
    join_paths(meson.current_source_dir(), preset),
    '-type', 'f',
    '-name', '*.gtp',
    '-printf', preset + '/%f\n'
  ).stdout().strip().split('\n')


  install_data(files,
    install_dir: join_paths(datadir, 'tool-presets', preset)
  )
endforeach
