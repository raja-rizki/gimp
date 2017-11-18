plugin_screenshot_sources = [
  'screenshot.c',
  'screenshot-gnome-shell.c',
  'screenshot-osx.c',
  'screenshot-x11.c',
  # 'screenshot-win32.rc',
  'screenshot-win32.c',
]

screenshot = executable('screenshot',
  plugin_screenshot_sources,
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl,
    x11, xmu, xext, xfixes,
  ],
  link_with: [
    libgimp,
    libgimpbase,
    libgimpcolor,
    libgimpconfig,
    libgimpmath,
    libgimpui,
    libgimpwidgets,
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)
