
apptests_includes = [
  rootInclude, rootAppInclude
]
apptests_deps = [
  pangocairo, gtk2, dbus_glib, gegl,
]
apptests_links = [
  # libapp,
  libappactions,
  libappconfig,
  libappcore,
  libappdialogs,
  libappdialogs,
  libappdisplay,
  libappfile,
  libappgegl,
  libappgui,
  libappinternalprocs,
  libapplayermodes,
  libapplayermodeslegacy,
  libappmenus,
  libappoperations,
  libapppaint,
  libapppdb,
  libappplugin,
  libapppropgui,
  libapptext,
  libapptools,
  libappvectors,
  libappwidgets,
  libappxcf,
]


libapptestutils = static_library('apptestutils',
  [
    'gimp-app-test-utils.c',
    'gimp-test-session-utils.c',
  ],
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)

apptests_links += libapptestutils

executable('test-core',
  'test-core.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-gimpidtable',
  'test-gimpidtable.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-save-and-export',
  'test-save-and-export.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-session-2-6-compatibility',
  'test-session-2-6-compatibility.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-session-2-8-compatibility-multi-window',
  'test-session-2-8-compatibility-multi-window.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-session-2-8-compatibility-single-window',
  'test-session-2-8-compatibility-single-window.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-single-window-mode',
  'test-single-window-mode.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-tools',
  'test-tools.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-ui',
  'test-ui.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)
executable('test-xcf',
  'test-xcf.c',
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)