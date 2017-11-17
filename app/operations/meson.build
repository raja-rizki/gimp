
appoperationsenums = custom_target('operations-enums.c',
  input : [ 'operations-enums.h', ],
  output: [ 'operations-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "core/core-enums.h"\n'+
              '#include "operations-enums.h"\n'+
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


libappoperations_sources = [
  'gimp-operation-config.c',
  'gimp-operations.c',
  'gimpbrightnesscontrastconfig.c',
  'gimpcageconfig.c',
  'gimpcolorbalanceconfig.c',
  'gimpcurvesconfig.c',
  'gimphuesaturationconfig.c',
  'gimplevelsconfig.c',
  'gimpoperationblend.c',
  'gimpoperationborder.c',
  'gimpoperationbrightnesscontrast.c',
  'gimpoperationcagecoefcalc.c',
  'gimpoperationcagetransform.c',
  'gimpoperationcolorbalance.c',
  'gimpoperationcolorize.c',
  'gimpoperationcomposecrop.c',
  'gimpoperationcurves.c',
  'gimpoperationdesaturate.c',
  'gimpoperationequalize.c',
  'gimpoperationflood.c',
  'gimpoperationgrow.c',
  'gimpoperationhistogramsink.c',
  'gimpoperationhuesaturation.c',
  'gimpoperationlevels.c',
  'gimpoperationmaskcomponents.c',
  'gimpoperationpointfilter.c',
  'gimpoperationposterize.c',
  'gimpoperationprofiletransform.c',
  'gimpoperationscalarmultiply.c',
  'gimpoperationsemiflatten.c',
  'gimpoperationsetalpha.c',
  'gimpoperationshapeburst.c',
  'gimpoperationshrink.c',
  'gimpoperationthreshold.c',
  'gimpoperationthresholdalpha.c',
  appoperationsenums
]

libappoperations = static_library('appoperations',
  libappoperations_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Operations"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf,
  ],
)

subdir('layer-modes')
subdir('layer-modes-legacy')
subdir('tests')
