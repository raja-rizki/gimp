
apptests_includes = [
  rootInclude, rootAppInclude
]
apptests_deps = [
  pangocairo, gtk2, dbus_glib, gegl,
]
apptests_links = [
  libapp,
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
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
  libgimpmath,
  libgimpmodule,
  libgimpthumb,
  libgimpwidgets,
]


libapptestutils_sources = [
  'gimp-app-test-utils.c',
  'gimp-test-session-utils.c',
]

libapptestutils = static_library('apptestutils',
  libapptestutils_sources,
  include_directories: apptests_includes,
  dependencies: apptests_deps,
  link_with: apptests_links,
)

apptests_links += libapptestutils


app_tests = [
  'test-core',
  'test-gimpidtable',
  'test-save-and-export',
  'test-session-2-6-compatibility',
  'test-session-2-8-compatibility-multi-window',
  'test-session-2-8-compatibility-single-window',
  'test-single-window-mode',
  'test-tools',
  'test-ui',
  'test-xcf',
]

foreach test_name : app_tests
  test_exe = executable(test_name,
    test_name + '.c',
    include_directories: apptests_includes,
    dependencies: apptests_deps,
    link_with: apptests_links,
  )

  test('app_' + test_name,
    test_exe,
    env: [
      'GIMP_TESTING_ABS_TOP_SRCDIR=' + meson.source_root(),
      'GIMP_TESTING_ABS_TOP_BUILDDIR=' + meson.build_root(),
      'GIMP_TESTING_PLUGINDIRS=' + join_paths(meson.build_root(), 'plug-ins', 'common'),
      'GIMP_TESTING_PLUGINDIRS_BASENAME_IGNORES=mkgen.pl',
    ],
    suite: 'app',
  )

endforeach
