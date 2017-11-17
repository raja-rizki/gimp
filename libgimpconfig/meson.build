
gimpconfigenums = custom_target('gimpconfigenums.c',
  input : [ 'gimpconfigenums.h', ],
  output: [ 'gimpconfigenums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "gimpconfigenums.h"\n'+
              '#include "libgimp/libgimp-intl.h"\n',
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
              '      gimp_type_set_translation_domain (type, GETTEXT_PACKAGE "-libgimp");\n'+
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


libgimpconfig_sources = [
  'gimpcolorconfig.c',
  'gimpconfig-deserialize.c',
  'gimpconfig-error.c',
  'gimpconfig-iface.c',
  'gimpconfig-path.c',
  'gimpconfig-serialize.c',
  'gimpconfig-utils.c',
  'gimpconfigwriter.c',
  'gimpscanner.c',
  gimpconfigenums
]

libgimpconfig_headers = [
  'gimpcolorconfig.h',
  'gimpconfig-deserialize.h',
  'gimpconfig-error.h',
  'gimpconfig-iface.h',
  'gimpconfig-params.h',
  'gimpconfig-path.h',
  'gimpconfig-serialize.h',
  'gimpconfig-utils.h',
  'gimpconfig.h',
  'gimpconfigenums.h',
  'gimpconfigtypes.h',
  'gimpconfigwriter.h',
  'gimpscanner.h',
]


libgimpconfig_cflags = [
  '-DG_LOG_DOMAIN="'+ 'LibGimpConfig' + '"',
  '-DGIMP_CONFIG_COMPILATION',
]

libgimpconfig_lflags = [
  libgimpbase,
  libgimpcolor,
  libgimpmath,
]

if os_win32
  libgimpconfig_lflags += ['-export-symbols', 'gimpconfig.def']
endif



libgimpconfig = library('gimpconfig-' + api_version,
  libgimpconfig_sources,
  include_directories: rootInclude,
  dependencies: [
    cairo, gdk_pixbuf, gegl, gio, gio_specific,
  ],
  c_args:     [ libgimp_cflags, libgimpconfig_cflags, ],
  link_with:  [ libgimp_lflags, libgimpconfig_lflags, ],
  install: true,
  version: so_version,
)

install_headers(
  libgimpconfig_headers,
  subdir: join_paths(gimp_api_name, 'libgimpconfig'),
)
