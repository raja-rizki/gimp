
gimpwidgetsenums = custom_target('gimpwidgetsenums.c',
  input : [ 'gimpwidgetsenums.h', ],
  output: [ 'gimpwidgetsenums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "gimpwidgetsenums.h"\n'+
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

gimpwidgetsmarshal = gnome.genmarshal('gimpwidgetsmarshal',
  prefix: '_gimp_widgets_marshal',
  sources: 'gimpwidgetsmarshal.list',
  install_header: false,
)

if gtk_mac_integration_ok
  gimppickbutton = 'gimppickbutton-quartz.c'
else
  gimppickbutton = 'gimppickbutton-default.c'
endif


libgimpwidgets_sources = [
  'gimp3migration.c',
  'gimpbrowser.c',
  'gimpbutton.c',
  'gimpcairo-utils.c',
  'gimpcellrenderercolor.c',
  'gimpcellrenderertoggle.c',
  'gimpchainbutton.c',
  'gimpcolorarea.c',
  'gimpcolorbutton.c',
  'gimpcolordisplay.c',
  'gimpcolordisplaystack.c',
  'gimpcolorhexentry.c',
  'gimpcolornotebook.c',
  'gimpcolorprofilechooserdialog.c',
  'gimpcolorprofilecombobox.c',
  'gimpcolorprofilestore.c',
  'gimpcolorprofileview.c',
  'gimpcolorscale.c',
  'gimpcolorscales.c',
  'gimpcolorselect.c',
  'gimpcolorselection.c',
  'gimpcolorselector.c',
  'gimpcontroller.c',
  'gimpdialog.c',
  'gimpeevl.c',
  'gimpenumcombobox.c',
  'gimpenumlabel.c',
  'gimpenumstore.c',
  'gimpenumwidgets.c',
  'gimpfileentry.c',
  'gimpframe.c',
  'gimphelpui.c',
  'gimphintbox.c',
  # 'gimpicons.c',
  'gimpintcombobox.c',
  'gimpintstore.c',
  'gimpmemsizeentry.c',
  'gimpnumberpairentry.c',
  'gimpoffsetarea.c',
  'gimpoldwidgets.c',
  'gimppageselector.c',
  'gimppatheditor.c',
  'gimppickbutton.c',
  'gimppixmap.c',
  'gimppreview.c',
  'gimppreviewarea.c',
  'gimppropwidgets.c',
  'gimpquerybox.c',
  'gimpruler.c',
  'gimpscaleentry.c',
  'gimpscrolledpreview.c',
  'gimpsizeentry.c',
  'gimpstringcombobox.c',
  'gimpunitcombobox.c',
  'gimpunitmenu.c',
  'gimpunitstore.c',
  'gimpwidgets-error.c',
  'gimpwidgets-private.c',
  'gimpwidgets.c',
  'gimpwidgetsutils.c',
  'gimpzoommodel.c',
  gimpwidgetsenums,
  gimpwidgetsmarshal,
  gimppickbutton,
]

libgimpwidgets_headers = [
  'gimp3migration.h',
  'gimpbrowser.h',
  'gimpbutton.h',
  'gimpcairo-utils.h',
  'gimpcellrenderercolor.h',
  'gimpcellrenderertoggle.h',
  'gimpchainbutton.h',
  'gimpcolorarea.h',
  'gimpcolorbutton.h',
  'gimpcolordisplay.h',
  'gimpcolordisplaystack.h',
  'gimpcolorhexentry.h',
  'gimpcolornotebook.h',
  'gimpcolorprofilechooserdialog.h',
  'gimpcolorprofilecombobox.h',
  'gimpcolorprofilestore.h',
  'gimpcolorprofileview.h',
  'gimpcolorscale.h',
  'gimpcolorscales.h',
  'gimpcolorselect.h',
  'gimpcolorselection.h',
  'gimpcolorselector.h',
  'gimpcontroller.h',
  'gimpdialog.h',
  'gimpenumcombobox.h',
  'gimpenumlabel.h',
  'gimpenumstore.h',
  'gimpenumwidgets.h',
  'gimpfileentry.h',
  'gimpframe.h',
  'gimphelpui.h',
  'gimphintbox.h',
  'gimpicons.h',
  'gimpintcombobox.h',
  'gimpintstore.h',
  'gimpmemsizeentry.h',
  'gimpnumberpairentry.h',
  'gimpoffsetarea.h',
  'gimpoldwidgets.h',
  'gimppageselector.h',
  'gimppatheditor.h',
  'gimppickbutton.h',
  'gimppixmap.h',
  'gimppreview.h',
  'gimppreviewarea.h',
  'gimppropwidgets.h',
  'gimpquerybox.h',
  'gimpruler.h',
  'gimpscaleentry.h',
  'gimpscrolledpreview.h',
  'gimpsizeentry.h',
  'gimpstringcombobox.h',
  'gimpunitcombobox.h',
  'gimpunitmenu.h',
  'gimpunitstore.h',
  'gimpwidgets-error.h',
  'gimpwidgets.h',
  'gimpwidgetsenums.h',
  'gimpwidgetstypes.h',
  'gimpwidgetsutils.h',
  'gimpzoommodel.h',
]


libgimpwidgets_cflags = [
  '-DG_LOG_DOMAIN="LibGimpWidgets"',
  '-DGIMP_WIDGETS_COMPILATION',
]

libgimpwidgets_lflags = [
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
]

if os_win32
  libgimpwidgets_lflags += ['-export-symbols', 'gimpwidgets.def']
  libgimpwidgets_lflags += '-lgdi32'
endif


libgimpwidgets = library('gimpwidgets-'+ api_version,
  libgimpwidgets_sources,
  include_directories: rootInclude,
  dependencies: [
    gegl, gtk2, lcms, math
  ],
  c_args:     [ libgimp_cflags, libgimpwidgets_cflags, ],
  link_with:  [ libgimp_lflags, libgimpwidgets_lflags, ],
)

install_headers(
  libgimpwidgets_headers,
  install_dir: join_paths(gimp_api_name, 'libgimpwidgets'),
)


# Test programs, not installed

test_preview_area = executable('test-preview-area',
  'test-preview-area.c',
  include_directories: rootInclude,
  dependencies: [
    gtk2,
  ],
  c_args:     [ libgimp_cflags, libgimpwidgets_cflags, ],
  link_with:  [ libgimp_lflags, libgimpwidgets_lflags, libgimpwidgets, ],
  install: false,
  build_by_default: false,
)

test_eevl = executable('test-eevl',
  'test-eevl.c',
  include_directories: rootInclude,
  dependencies: [
    glib, gtk2,
  ],
  c_args:     [ libgimp_cflags, libgimpwidgets_cflags, ],
  link_with:  [ libgimp_lflags, libgimpwidgets_lflags, libgimpwidgets, ],
  install: false,
)
