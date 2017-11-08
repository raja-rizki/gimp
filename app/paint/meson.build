libapppaint_sources = [
  'gimp-paint.c',
  'gimpairbrush.c',
  'gimpairbrushoptions.c',
  'gimpbrushcore.c',
  'gimpclone.c',
  'gimpcloneoptions.c',
  'gimpconvolve.c',
  'gimpconvolveoptions.c',
  'gimpdodgeburn.c',
  'gimpdodgeburnoptions.c',
  'gimperaser.c',
  'gimperaseroptions.c',
  'gimpheal.c',
  'gimpink-blob.c',
  'gimpink.c',
  'gimpinkoptions.c',
  'gimpinkundo.c',
  'gimpmybrushcore.c',
  'gimpmybrushoptions.c',
  'gimpmybrushsurface.c',
  'gimppaintbrush.c',
  'gimppaintcore-loops.c',
  'gimppaintcore-stroke.c',
  'gimppaintcore.c',
  'gimppaintcoreundo.c',
  'gimppaintoptions.c',
  'gimppencil.c',
  'gimppenciloptions.c',
  'gimpperspectiveclone.c',
  'gimpperspectivecloneoptions.c',
  'gimpsmudge.c',
  'gimpsmudgeoptions.c',
  'gimpsourcecore.c',
  'gimpsourceoptions.c',
]

# TODO mkenums
libapppaint_sources += [
  'paint-enums.c',
]

libapppaint = static_library('apppaint',
  libapppaint_sources,
  include_directories: [ rootInclude, rootAppInclude, ],
  c_args: [
    '-DG_LOG_DOMAIN="Gimp-Paint"',
  ],
  dependencies: [
    cairo, gegl, gdk_pixbuf, libmypaint,
  ],
)
