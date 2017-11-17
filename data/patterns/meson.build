patterns = run_command('find',
  meson.current_source_dir(),
  '-maxdepth', '1',
  '-mindepth', '1',
  '-type', 'd',
  '-printf', '%f\n'
).stdout().strip().split('\n')

foreach pattern : patterns
  files = run_command('find',
    join_paths(meson.current_source_dir(), pattern),
    '-type', 'f',
    '-name', '*.pat',
    '-printf', pattern + '/%f\n'
  ).stdout().strip().split('\n')


  install_data(files,
    install_dir: join_paths(gimpdatadir, 'patterns', pattern)
  )
endforeach
