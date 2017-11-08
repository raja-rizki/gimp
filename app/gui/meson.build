libappgui_sources = [
  # 'gimpdbusservice.c',
  'gimpuiconfigurer.c',
  'gui-message.c',
  # 'gui-unique.c',
  'gui-vtable.c',
  'gui.c',
  'icon-themes.c',
  'session.c',
  'splash.c',
  'themes.c',
]

# TODO dbus-codegen
libappgui_sources += [
  # 'gimpdbusservice-generated.c',
]

libappgui = static_library('appgui',
  libappgui_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-GUI"',
    '-DGIMP_COMMAND="'+ gimp_command +'"',
  ],
  dependencies: [
    cairo, dbus_glib, gegl, gdk_pixbuf, gio_specific, gtk2
  ],
)
