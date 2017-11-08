libappplugin_sources = [
  'gimpenvirontable.c',
  'gimpinterpreterdb.c',
  'gimpplugin-cleanup.c',
  'gimpplugin-context.c',
  'gimpplugin-message.c',
  'gimpplugin-progress.c',
  'gimpplugin.c',
  'gimpplugindebug.c',
  'gimpplugindef.c',
  'gimppluginerror.c',
  'gimppluginmanager-call.c',
  'gimppluginmanager-data.c',
  'gimppluginmanager-file-procedure.c',
  'gimppluginmanager-file.c',
  'gimppluginmanager-help-domain.c',
  'gimppluginmanager-locale-domain.c',
  'gimppluginmanager-menu-branch.c',
  'gimppluginmanager-query.c',
  'gimppluginmanager-restore.c',
  'gimppluginmanager.c',
  'gimppluginprocedure.c',
  'gimppluginprocframe.c',
  'gimppluginshm.c',
  'gimptemporaryprocedure.c',
  'plug-in-menu-path.c',
  'plug-in-params.c',
  'plug-in-rc.c',
]

# TODO mkenums
libappplugin_sources += [
  'plug-in-enums.c',
]

libappplugin = static_library('appplug-in',
  libappplugin_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Plug-In"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf,
  ],
)
