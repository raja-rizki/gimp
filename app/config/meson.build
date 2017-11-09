
appconfigenums = custom_target('config-enums.c',
  input : [ 'config-enums.h', ],
  output: [ 'config-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "config-enums.h"\n'+
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

libappconfig_sources = [
  'gimpconfig-dump.c',
  'gimpconfig-file.c',
  'gimpconfig-utils.c',
  'gimpcoreconfig.c',
  'gimpdialogconfig.c',
  'gimpdisplayconfig.c',
  'gimpdisplayoptions.c',
  'gimpgeglconfig.c',
  'gimpguiconfig.c',
  'gimplangrc.c',
  'gimppluginconfig.c',
  'gimprc-deserialize.c',
  'gimprc-serialize.c',
  'gimprc-unknown.c',
  'gimprc.c',
  'gimpxmlparser.c',
  appconfigenums,
]

libappconfig = static_library('appconfig',
  libappconfig_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Config"',
    '-DGIMP_APP_VERSION_STRING="'+ app_version +'"',
    '-DDATADIR="'+ datadir +'"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf, gio, gio_specific, gtk2,
  ],
)


executable('test-config',
  [ 'test-config.c', app_debug_files, ],
  include_directories: [ rootInclude, rootAppInclude, ],

  dependencies: [
    gegl, gio, gio_specific,
  ],
  link_with: [
    libgimpbase,
    libgimpconfig,
    libgimpcolor,
    libgimpmath,
    libgimpmodule,
    libgimpthumb,

    libappcore,
    libappconfig,
    libappfile,
    libappgegl,
    libappinternalprocs,
    libapplayermodes,
    libapplayermodeslegacy,
    libappoperations,
    libapppaint,
    libapppdb,
    libappplugin,
    libapptext,
    libappvectors,
    libappxcf,
  ],
  install: false,
)
