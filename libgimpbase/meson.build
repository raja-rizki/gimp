
gimpbaseenums = custom_target('gimpbaseenums.c',
  input : [ 'gimpbaseenums.h', ],
  output: [ 'gimpbaseenums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <glib-object.h>\n'+
              '#undef GIMP_DISABLE_DEPRECATED\n'+
              '#include "gimpbasetypes.h"\n'+
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
gimpcompatenums = custom_target('gimpcompatenums.c',
  input : [ 'gimpcompatenums.h', ],
  output: [ 'gimpcompatenums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <glib-object.h>\n'+
              '#include "gimpbasetypes.h"\n'+
              '#include "gimpcompatenums.h"\n'+
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

libgimpbase_sources = [
  'gimpbase-private.c',
  'gimpbasetypes.c',
  'gimpchecks.c',
  'gimpcpuaccel.c',
  'gimpdatafiles.c',
  'gimpenv.c',
  'gimpmemsize.c',
  'gimpmetadata.c',
  'gimpparasite.c',
  'gimpparasiteio.c',
  'gimpprotocol.c',
  'gimprectangle.c',
  'gimpreloc.c',
  'gimpsignal.c',
  'gimpunit.c',
  'gimputils.c',
  'gimpvaluearray.c',
  'gimpwire.c',
  gimpbaseenums,
  gimpcompatenums,
]

libgimpbase_headers = [
  'gimpbase.h',
  'gimpbaseenums.h',
  'gimpbasetypes.h',
  'gimpcpuaccel.h',
  'gimplimits.h',
  'gimpparam.h',
  'gimpversion.h',
  'gimpchecks.h',
  'gimpdatafiles.h',
  'gimpenv.h',
  'gimpmemsize.h',
  'gimpmetadata.h',
  'gimpparasite.h',
  'gimpparasiteio.h',
  'gimprectangle.h',
  'gimpsignal.h',
  'gimpunit.h',
  'gimputils.h',
  'gimpvaluearray.h',
]

libgimpbase_cflags = [
  '-DG_LOG_DOMAIN="LibGimpBase"',
  '-DGIMP_BASE_COMPILATION',
]
libgimpbase_lflags = [ ]

if os_win32
  libgimpbase_lflags += '-lole32'
  libgimpbase_lflags += ['-export-symbols', 'gimpbase.def']
endif


libgimpbase = library('gimpbase-' + api_version,
  libgimpbase_sources,
  include_directories: rootInclude,
  dependencies: [
    gexiv2, gio, math,
  ],
  c_args:     [ libgimp_cflags, libgimpbase_cflags, ],
  link_with:  [ libgimp_lflags, libgimpbase_lflags, ],
)

install_headers(
  libgimpbase_headers,
  install_dir: join_paths(gimp_api_name, 'libgimpbase'),
)


# Test program, not installed
executable('test-cpu-accel',
  'test-cpu-accel.c',
  include_directories: rootInclude,
  dependencies: [
    glib,
  ],
  c_args:     [ libgimp_cflags, libgimpbase_cflags, ],
  link_with:  [ libgimp_lflags, libgimpbase_lflags, libgimpbase, ],
  install: false,
)
