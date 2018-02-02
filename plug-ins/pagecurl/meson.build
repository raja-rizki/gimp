pagecurl_icons_images = [
  'curl0.png',
  'curl1.png',
  'curl2.png',
  'curl3.png',
  'curl4.png',
  'curl5.png',
  'curl6.png',
  'curl7.png',
]
resourcename = 'pagecurl-icons'
xml_content  = '<?xml version="1.0" encoding="UTF-8"?>\n'
xml_content += '<gresources>\n'
xml_content += '  <gresource prefix="/org/gimp/icons">\n'
foreach file : pagecurl_icons_images
  xml_content+='    <file preprocess="to-pixdata">'+ file +'</file>\n'
endforeach
xml_content += '  </gresource>\n'
xml_content += '</gresources>\n'

xml_file = configure_file(
  output: resourcename + '.gresource.xml',
  command: [ 'echo', xml_content ],
  capture: true,
)

pagecurl_icons_sources = gnome.compile_resources(
  resourcename,
  xml_file,
  c_name: resourcename.underscorify(),
)


plugin_pagecurl_sources = [
  'pagecurl.c',
  pagecurl_icons_sources,
]
# TODO pagecurl.rc.o

pagecurl = executable('pagecurl',
  plugin_pagecurl_sources,
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl, math,
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
  c_args: [
    '-DMESON_BUILD',
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)
