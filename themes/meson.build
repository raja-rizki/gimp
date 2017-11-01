themes = run_command('find',
  meson.current_source_dir(),
  '-maxdepth', '1',
  '-mindepth', '1',
  '-type', 'd',
  '-printf', '%f\n'
).stdout().strip().split('\n')

foreach theme : themes
  install_data(
    join_paths(theme, 'gtkrc'),
    install_dir: join_paths(datadir, 'themes', theme)
  )

  if run_command('[', '-d', join_paths(theme, 'ui'), ']').returncode() == 0
    install_subdir(
      join_paths(theme, 'ui'),
      install_dir: join_paths(datadir, 'themes', theme)
    )
  endif
endforeach