
appdisplayenums = custom_target('display-enums.c',
  input : [ 'display-enums.h', ],
  output: [ 'display-enums.c', ],
  command: [
    gimp_mkenums,
    '--fhead','#include "config.h"\n'+
              '#include <gio/gio.h>\n'+
              '#include "libgimpbase/gimpbase.h"\n'+
              '#include "display-enums.h"\n'+
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

libappdisplay_sources = [
  'gimpcanvas-style.c',
  'gimpcanvas.c',
  'gimpcanvasarc.c',
  'gimpcanvasboundary.c',
  'gimpcanvasbufferpreview.c',
  'gimpcanvascorner.c',
  'gimpcanvascursor.c',
  'gimpcanvasgrid.c',
  'gimpcanvasgroup.c',
  'gimpcanvasguide.c',
  'gimpcanvashandle.c',
  'gimpcanvasitem-utils.c',
  'gimpcanvasitem.c',
  'gimpcanvaslayerboundary.c',
  'gimpcanvasline.c',
  'gimpcanvaspassepartout.c',
  'gimpcanvaspath.c',
  'gimpcanvaspen.c',
  'gimpcanvaspolygon.c',
  'gimpcanvasprogress.c',
  'gimpcanvasproxygroup.c',
  'gimpcanvasrectangle.c',
  'gimpcanvasrectangleguides.c',
  'gimpcanvassamplepoint.c',
  'gimpcanvastextcursor.c',
  'gimpcanvastransformguides.c',
  'gimpcanvastransformpreview.c',
  'gimpcursorview.c',
  'gimpdisplay-foreach.c',
  'gimpdisplay-handlers.c',
  'gimpdisplay.c',
  'gimpdisplayshell-actions.c',
  'gimpdisplayshell-appearance.c',
  'gimpdisplayshell-autoscroll.c',
  'gimpdisplayshell-callbacks.c',
  'gimpdisplayshell-close.c',
  'gimpdisplayshell-cursor.c',
  'gimpdisplayshell-dnd.c',
  'gimpdisplayshell-draw.c',
  'gimpdisplayshell-expose.c',
  'gimpdisplayshell-filter-dialog.c',
  'gimpdisplayshell-filter.c',
  'gimpdisplayshell-grab.c',
  'gimpdisplayshell-handlers.c',
  'gimpdisplayshell-icon.c',
  'gimpdisplayshell-items.c',
  'gimpdisplayshell-layer-select.c',
  'gimpdisplayshell-profile.c',
  'gimpdisplayshell-progress.c',
  'gimpdisplayshell-render.c',
  'gimpdisplayshell-rotate-dialog.c',
  'gimpdisplayshell-rotate.c',
  'gimpdisplayshell-rulers.c',
  'gimpdisplayshell-scale-dialog.c',
  'gimpdisplayshell-scale.c',
  'gimpdisplayshell-scroll.c',
  'gimpdisplayshell-scrollbars.c',
  'gimpdisplayshell-selection.c',
  'gimpdisplayshell-title.c',
  'gimpdisplayshell-tool-events.c',
  'gimpdisplayshell-transform.c',
  'gimpdisplayshell.c',
  'gimpdisplayxfer.c',
  'gimpimagewindow.c',
  'gimpmotionbuffer.c',
  'gimpmultiwindowstrategy.c',
  'gimpnavigationeditor.c',
  'gimpscalecombobox.c',
  'gimpsinglewindowstrategy.c',
  'gimpstatusbar.c',
  'gimptoolcompass.c',
  'gimptooldialog.c',
  'gimptoolgui.c',
  'gimptoolhandlegrid.c',
  'gimptoolline.c',
  'gimptoolpath.c',
  'gimptoolpolygon.c',
  'gimptoolrectangle.c',
  'gimptoolrotategrid.c',
  'gimptoolsheargrid.c',
  'gimptooltransformgrid.c',
  'gimptoolwidget.c',
  appdisplayenums,
  gitversion_h,
]

libappdisplay = static_library('appdisplay',
  libappdisplay_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Display"',
  ],
  dependencies: [
    gegl, gtk2,
  ],
)
