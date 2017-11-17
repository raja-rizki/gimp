
# Configure_file is just here to rename the files
manconf = configuration_data()

man_files = [
  configure_file(
    input : 'gimptool.1.in',
    output: 'gimptool-' + tool_version + '.1',
    configuration: manconf,
  ),
  configure_file(
    input : 'gimprc.5.in',
    output: 'gimprc-' + app_version + '.5',
    configuration: manconf,
  ),
]

if enable_console_bin
  man_files += configure_file(
    input : 'gimp.1.in',
    output: 'gimp-console' + app_version + '.1',
    configuration: manconf,
  )
endif

if enable_default_bin
  man_files +=  configure_file(
    input : 'gimp.1.in',
    output: 'gimp-' + app_version + '.1',
    configuration: manconf,
  )
endif

install_man(man_files)
