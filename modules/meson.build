
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

libcolor_selector_cmyk = library('color-selector-cmyk',
  'color-selector-cmyk.c',
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: color_selector_libs,
)

libcolor_selector_water = library('color-selector-water',
  'color-selector-water.c',
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: color_selector_libs,
)

libcolor_selector_wheel = library('color-selector-wheel',
  [
    'color-selector-wheel.c',
    'gimpcolorwheel.c',
  ],
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: color_selector_libs,
)

if have_linuxinput
libcontroller_linux_input = library('controller-linux-input',
  [
    'controller-linux-input.c',
    'gimpinputdevicestore-gudev.c',
  ],
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: controller_libs,
)
endif
if have_directXinput
libcontroller_dx_input = library('controller-dx-input',
  [
    'controller-dx-dinput.c',
    'gimpinputdevicestore-dx.c',
  ],
  include_directories: rootInclude,
  dependencies: [modules_deps, directx],
  link_with: [controller_libs, '-lrpcrt4'],
)

endif
if not platform_win32
libcontroller_midi = library('controller-midi',
  'controller-midi.c',
  include_directories: rootInclude,
  dependencies:modules_deps,
  link_with: controller_libs,
)
endif

libdisplay_filter_color_blind = library('display-filter-color-blind',
  'display-filter-color-blind.c',
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: display_filter_libs,
)

libdisplay_filter_gamma = library('display-filter-gamma',
  'display-filter-gamma.c',
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: display_filter_libs,
)

libdisplay_filter_high_contrast = library('display-filter-high-contrast',
  'display-filter-high-contrast.c',
  include_directories: rootInclude,
  dependencies: modules_deps,
  link_with: display_filter_libs,
)
