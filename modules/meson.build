
global_cflags = []
global_lflags = []

global_cflags += [
]

if platform_win32
  global_cflags += '-no-undefined'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  # global_lflags += ['-export-symbols', 'gimpmath.def']
endif

modules_deps = [
  gtk2, babl, gegl,
]

color_selector_libs = [
  libgimpcolor,
  libgimpconfig,
  libgimpmodule,
  libgimpwidgets,
]
controller_libs = [
  libgimpmodule,
  libgimpwidgets,
]
display_filter_libs = [
  libgimpbase,
  libgimpcolor,
  libgimpconfig,
  libgimpmodule,
  libgimpwidgets,
]

# Name, Sources, deps, link.
modules = [
  [ 'color-selector-cmyk',
    [ 'color-selector-cmyk.c', ],
    [], [ color_selector_libs, ],
  ],
  [ 'color-selector-water',
    [ 'color-selector-water.c', ],
    [], [ color_selector_libs, ],
  ],
  [ 'color-selector-wheel',
    [ 'color-selector-wheel.c', 'gimpcolorwheel.c', ],
    [], [ color_selector_libs, ],
  ],
  [ 'display-filter-clip-warning',
    [ 'display-filter-clip-warning.c', ],
    [], [ display_filter_libs, '-avoid-version', '-module', ],
  ],
  [ 'display-filter-color-blind',
    [ 'display-filter-color-blind.c', ],
    [], [ display_filter_libs, ],
  ],
  [ 'display-filter-gamma',
    [ 'display-filter-gamma.c', ],
    [], [ display_filter_libs, ],
  ],
  [ 'display-filter-high-contrast',
    [ 'display-filter-high-contrast.c', ],
    [], [ display_filter_libs, ],
  ],
]

if have_linuxinput
  modules += [
    [ 'controller-linux-input',
      [ 'controller-linux-input.c', 'gimpinputdevicestore-gudev.c', ],
      [], [ controller_libs, ],
    ],
  ]
endif

if have_directXinput
  modules += [
    [ 'controller-dx-input',
      [ 'controller-dx-dinput.c', 'gimpinputdevicestore-dx.c', ],
      [ directx,  ], [ controller_libs, '-lrpcrt4', ],
    ],
  ]
endif

if not platform_win32
  modules += [
    [ 'controller-midi',
      [ 'controller-midi.c', ],
      [], [ controller_libs, ],
    ],
  ]
endif


foreach module : modules
  library(module[0],
    module[1],
    include_directories: rootInclude,
    dependencies: modules_deps + module[2],
    link_with: module[3],
    install: true,
    install_dir: join_paths(gimpplugindir, 'modules'),
  )
endforeach
