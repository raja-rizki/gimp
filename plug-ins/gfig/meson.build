subdir('images')
# TODO gfig.rc.o

gfig = executable('gfig',
  [
    'gfig-arc.c',
    'gfig-bezier.c',
    'gfig-circle.c',
    'gfig-dialog.c',
    'gfig-dobject.c',
    'gfig-ellipse.c',
    'gfig-grid.c',
    'gfig-line.c',
    'gfig-poly.c',
    'gfig-preview.c',
    'gfig-rectangle.c',
    'gfig-spiral.c',
    'gfig-star.c',
    'gfig-stock.c',
    'gfig-style.c',
    'gfig.c',
    stock_pixbufs_h,
  ],
  include_directories: [ rootInclude, ],
  dependencies: [
    gtk2, gegl,
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
