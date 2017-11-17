
appgeglenums = custom_target('gimp-gegl-enums.c',
  input : [ 'gimp-gegl-enums.h', ],
  output: [ 'gimp-gegl-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "core/core-enums.h"\n'+
              '#include "gimp-gegl-enums.h"\n'+
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

libappgegl_sources = [
  'gimp-babl-compat.c',
  'gimp-babl.c',
  'gimp-gegl-apply-operation.c',
  'gimp-gegl-loops-sse2.c',
  'gimp-gegl-loops.c',
  'gimp-gegl-mask-combine.c',
  'gimp-gegl-mask.c',
  'gimp-gegl-nodes.c',
  'gimp-gegl-tile-compat.c',
  'gimp-gegl-utils.c',
  'gimp-gegl.c',
  'gimpapplicator.c',
  'gimptilehandlervalidate.c',
  appgeglenums,
]

libappgegl = static_library('appgegl',
  libappgegl_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-GEGL"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf,
  ],
)
