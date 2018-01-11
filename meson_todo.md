Meson Port
-----------

# Changes in existing files

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


# Changes in installed files
* gimpversion.h uses #pragma once
* `*.pc` cleaned up
  - exec_prefix removed
  - gimplocaledir, gimpdatadir relative to prefix, not datarootdir
  - required version added


# TODO

## Windows
* Windres generator for plugins `*.rc`


## Missing
* icons/Symbolic-Inverted
* tools/pdbgen
* translations in `appdata/*.xml`, `tips/gimp-tips.xml`
* gtkrc : missing python-fu-console ??
* man : XDG_CONFIG_HOME are replaced with /usr ??

# Sizes mismatches
plug-ins -> some have 4k added
