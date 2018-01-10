Meson Port
-----------

# Changes

## Generate headers instead of .c files.
* app/core/gimpviewable.c
```
+#ifdef MESON_BUILD
+#include "icons/Color/gimp-core-pixbufs.h"
+#else
 #include "icons/Color/gimp-core-pixbufs.c"
+#endif
```

* libgimpwidgets/gimpicons.c
```
+#ifdef MESON_BUILD
+#include "icons/Color/gimp-icon-pixbufs.h"
+#else
 #include "icons/Color/gimp-icon-pixbufs.c"
+#endif
```

* plug-ins/pagecurl/pagecurl.c
```
+#ifdef MESON_BUILD
+#include "pagecurl-icons.h"
+#else
 #include "pagecurl-icons.c"
+#endif
```

## Encoding fixes
* app/display/gimpdisplayshell-title.c

## Correctly detect Python2. Fix tab/spaces inconsistency.
* plug-ins/pygimp/py-compile


# TODO

## Windows
* Windres generator for plugins `*.rc`


## Missing
* icons/Symbolic-Inverted
* tools/pdbgen
