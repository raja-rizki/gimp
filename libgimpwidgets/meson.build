
global_cflags = []
global_lflags = []

global_cflags += [
]

if platform_win32
  global_cflags += '-no-undefined'
  global_lflags += '-lgdi32'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  # global_lflags += '-lole32'
  # global_lflags += ['-export-symbols', 'gimpwidgets.def']
endif


global_cflags += [
  '-DG_LOG_DOMAIN="'+ 'LibGimpWidgets' + '"',
  '-DGIMP_WIDGETS_COMPILATION',
]




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
  'gimpicons.c',
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
]

if gtk_mac_integration_ok
  libgimpwidgets_sources += 'gimppickbutton-quartz.c'
  global_cflags += '-xobjective-c'
else
  libgimpwidgets_sources += 'gimppickbutton-default.c'
endif

# TODO mkenums
libgimpwidgets_sources += [
  'gimpwidgetsenums.c',
  'gimpwidgetsmarshal.c',
  'gimpwidgetsmarshal.h',
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


libgimpwidgets = library('gimpwidgets-'+ api_version,
  libgimpwidgets_sources,
  include_directories: rootInclude,
  dependencies: [
    gegl, gtk2, lcms, math
  ],
  c_args: global_cflags,
  link_with: [ global_lflags, libgimpbase, libgimpcolor, libgimpconfig, ],
)

install_headers(
  libgimpwidgets_headers,
  install_dir: join_paths('gimp-' + api_version, 'libgimpwidgets'),
)


# test programs, not installed

# test_preview_area = executable('test-preview-area',
#   'test-preview-area.c',
#   include_directories: rootInclude,
#   dependencies: [
#     gtk2,
#   ],
#   c_args: global_cflags,
#   link_with: libgimpbase,
#   install: false,
# )

test_eevl = executable('test-eevl',
  'test-eevl.c',
  include_directories: rootInclude,
  dependencies: [
    glib, gtk2,
  ],
  c_args: global_cflags,
  link_with: [ libgimpcolor, libgimpwidgets, ],
  install: false,
)
