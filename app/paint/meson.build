
apppaintenums = custom_target('paint-enums.c',
  input : [ 'paint-enums.h', ],
  output: [ 'paint-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "core/core-enums.h"\n'+
              '#include "paint-enums.h"\n'+
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


libapppaint_sources = [
  'gimp-paint.c',
  'gimpairbrush.c',
  'gimpairbrushoptions.c',
  'gimpbrushcore.c',
  'gimpclone.c',
  'gimpcloneoptions.c',
  'gimpconvolve.c',
  'gimpconvolveoptions.c',
  'gimpdodgeburn.c',
  'gimpdodgeburnoptions.c',
  'gimperaser.c',
  'gimperaseroptions.c',
  'gimpheal.c',
  'gimpink-blob.c',
  'gimpink.c',
  'gimpinkoptions.c',
  'gimpinkundo.c',
  'gimpmybrushcore.c',
  'gimpmybrushoptions.c',
  'gimpmybrushsurface.c',
  'gimppaintbrush.c',
  'gimppaintcore-loops.c',
  'gimppaintcore-stroke.c',
  'gimppaintcore.c',
  'gimppaintcoreundo.c',
  'gimppaintoptions.c',
  'gimppencil.c',
  'gimppenciloptions.c',
  'gimpperspectiveclone.c',
  'gimpperspectivecloneoptions.c',
  'gimpsmudge.c',
  'gimpsmudgeoptions.c',
  'gimpsourcecore.c',
  'gimpsourceoptions.c',
  apppaintenums
]

libapppaint = static_library('apppaint',
  libapppaint_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Paint"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf, libmypaint,
  ],
)
