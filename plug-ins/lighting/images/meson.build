stock_icons = [
  'stock-intensity-ambient-high',
  'stock-intensity-ambient-low',
  'stock-intensity-diffuse-high',
  'stock-intensity-diffuse-low',
  'stock-reflectivity-diffuse-high',
  'stock-reflectivity-diffuse-low',
  'stock-reflectivity-specular-high',
  'stock-reflectivity-specular-low',
  'stock-reflectivity-highlight-high',
  'stock-reflectivity-highlight-low',
]

stock_icons_list = []
foreach name : stock_icons
  stock_icons_list += name.underscorify()
  stock_icons_list += join_paths(
    meson.source_root(),
    meson.current_source_dir(),
    name + '.png'
  )
endforeach

message(stock_icons_list)

gdk_pixbuf_csource = find_program('gdk-pixbuf-csource')

stock_pixbufs_h = custom_target('stock-pixbufs.h',
  input : [ ],
  output: [ 'stock-pixbufs.h', ],
  command: [
    gdk_pixbuf_csource,
    '--raw',
    '--build-list',
    stock_icons_list,
  ],
  capture: true,
)

# stock-icons.list: $(STOCK_IMAGES) Makefile.am
# 	( rm -f $@; \
#           for image in $(STOCK_IMAGES); do \
#             echo $$image | \
#               sed -e 's|.*/||' -e 's|-|_|g' -e 's|\.png$$||' >> $@; \
# 	    echo "  $(srcdir)/$$image" >> $@; \
# 	  done )
#
# $(srcdir)/stock-pixbufs.h: stock-icons.list
# 	$(GDK_PIXBUF_CSOURCE) --raw --build-list `cat stock-icons.list` > $(@F)
