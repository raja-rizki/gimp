
apppluginenums = custom_target('plug-in-enums.c',
  input : [ 'plug-in-enums.h', ],
  output: [ 'plug-in-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "core/core-enums.h"\n'+
              '#include "plug-in-enums.h"\n'+
              '#include"gimp-intl.h"\n',
    '--fprod','/* enumerations from "@basename@" */\n',
    '--vhead','GType\n'+
              '@enum_name@_get_type (void)\n'+
              '{\n'+
              '  static const G@Type@Value values[] =\n'+
              '  {',
    '--vprod','    { @VALUENAME@, "@VALUENAME@", "@valuenick@" },',
    '--vtail','    { 0, NULL, NULL }\n'+
              '  };\n',
    '--dhead','  static const Gimp@Type@Desc descs[] =\n'+
              '  {',
    '--dprod','    { @VALUENAME@, @valuedesc@, @valuehelp@ },',
    '--dtail','    { 0, NULL, NULL }\n'+
              '  };\n'+
              '\n'+
              '  static GType type = 0;\n'+
              '\n'+
              '  if (G_UNLIKELY (! type))\n'+
              '    {\n'+
              '      type = g_@type@_register_static ("@EnumName@", values);\n'+
              '      gimp_type_set_translation_context (type, "@enumnick@");\n'+
              '      gimp_@type@_set_value_descriptions (type, descs);\n'+
              '    }\n'+
              '\n'+
              '  return type;\n'+
              '}\n',
    '@INPUT@',
  ],
  capture: true,
)


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
  apppluginenums,
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
