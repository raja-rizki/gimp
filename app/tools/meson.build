
apptoolsenums = custom_target('tools-enums.c',
  input : [ 'tools-enums.h', ],
  output: [ 'tools-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "core/core-enums.h"\n'+
              '#include "tools-enums.h"\n'+
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

libapptools_sources = [
  'gimp-tools.c',
  'gimpairbrushtool.c',
  'gimpalignoptions.c',
  'gimpaligntool.c',
  'gimpblendoptions.c',
  'gimpblendtool-editor.c',
  'gimpblendtool.c',
  'gimpbrightnesscontrasttool.c',
  'gimpbrushtool.c',
  'gimpbucketfilloptions.c',
  'gimpbucketfilltool.c',
  'gimpbycolorselecttool.c',
  'gimpcageoptions.c',
  'gimpcagetool.c',
  'gimpcloneoptions-gui.c',
  'gimpclonetool.c',
  'gimpcoloroptions.c',
  'gimpcolorpickeroptions.c',
  'gimpcolorpickertool.c',
  'gimpcolortool.c',
  'gimpconvolvetool.c',
  'gimpcropoptions.c',
  'gimpcroptool.c',
  'gimpcurvestool.c',
  'gimpdodgeburntool.c',
  'gimpdrawtool.c',
  'gimpeditselectiontool.c',
  'gimpellipseselecttool.c',
  'gimperasertool.c',
  'gimpfilteroptions.c',
  'gimpfiltertool-settings.c',
  'gimpfiltertool-widgets.c',
  'gimpfiltertool.c',
  'gimpflipoptions.c',
  'gimpfliptool.c',
  'gimpforegroundselectoptions.c',
  'gimpforegroundselecttool.c',
  'gimpforegroundselecttoolundo.c',
  'gimpfreeselecttool.c',
  'gimpfuzzyselecttool.c',
  'gimpgegltool.c',
  'gimpguidetool.c',
  'gimphandletransformoptions.c',
  'gimphandletransformtool.c',
  'gimphealtool.c',
  'gimphistogramoptions.c',
  'gimpinkoptions-gui.c',
  'gimpinktool.c',
  'gimpiscissorsoptions.c',
  'gimpiscissorstool.c',
  'gimplevelstool.c',
  'gimpmagnifyoptions.c',
  'gimpmagnifytool.c',
  'gimpmeasureoptions.c',
  'gimpmeasuretool.c',
  'gimpmoveoptions.c',
  'gimpmovetool.c',
  'gimpmybrushoptions-gui.c',
  'gimpmybrushtool.c',
  'gimpnpointdeformationoptions.c',
  'gimpnpointdeformationtool.c',
  'gimpoperationtool.c',
  'gimppaintbrushtool.c',
  'gimppaintoptions-gui.c',
  'gimppainttool.c',
  'gimppenciltool.c',
  'gimpperspectiveclonetool.c',
  'gimpperspectivetool.c',
  'gimprectangleoptions.c',
  'gimprectangleselectoptions.c',
  'gimprectangleselecttool.c',
  'gimpregionselectoptions.c',
  'gimpregionselecttool.c',
  'gimprotatetool.c',
  'gimpsamplepointtool.c',
  'gimpscaletool.c',
  'gimpseamlesscloneoptions.c',
  'gimpseamlessclonetool.c',
  'gimpselectionoptions.c',
  'gimpselectiontool.c',
  'gimpsheartool.c',
  'gimpsmudgetool.c',
  'gimpsourcetool.c',
  'gimptextoptions.c',
  'gimptexttool-editor.c',
  'gimptexttool.c',
  'gimpthresholdtool.c',
  'gimptilehandleriscissors.c',
  'gimptool-progress.c',
  'gimptool.c',
  'gimptoolcontrol.c',
  'gimptooloptions-gui.c',
  'gimptransformoptions.c',
  'gimptransformtool.c',
  'gimptransformtoolundo.c',
  'gimpunifiedtransformtool.c',
  'gimpvectoroptions.c',
  'gimpvectortool.c',
  'gimpwarpoptions.c',
  'gimpwarptool.c',
  'tool_manager.c',
  apptoolsenums
]

libapptools = static_library('apptools',
  libapptools_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Tools"',
  ],
  dependencies: [
    gegl, gtk2,
  ],
)

