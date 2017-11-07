
global_cflags = []
global_lflags = []



global_cflags += [
  '-DPREFIX="'+ prefix + '"',
  '-DGIMPDIR="'+ gimpdir + '"',
  '-DDATADIR="'+ datadir + '"',
  '-DLOCALEDIR="'+ localedir + '"',
  '-DPLUGINDIR="'+ plugindir + '"',
  '-DSYSCONFDIR="'+ sysconfdir + '"',
  '-DGIMP_PACKAGE="'+ gettext_package + '"',
  '-DGIMP_DATA_VERSION="'+ data_version + '"',
  '-DGIMP_USER_VERSION="'+ user_version + '"',
  '-DGIMP_SYSCONF_VERSION="'+ sysconf_version + '"',
  '-DGIMP_PLUGIN_VERSION="'+ plugin_version + '"',
  '-DG_LOG_DOMAIN="'+ 'LibGimpBase' + '"',
  '-DGIMP_BASE_COMPILATION',
]


if platform_win32
  global_cflags += '-no-undefined'
endif

if platform_osx
  global_cflags += '-xobjective-c'
  global_lflags += ['-framework', 'Cocoa']
endif

if os_win32
  global_lflags += '-lole32'
  # global_lflags += ['-export-symbols', 'gimpbase.def']
endif

#  $(GIO_CFLAGS)						\
# $(GEXIV2_CFLAGS)					\
# $(BINRELOC_CFLAGS)					\
# $(xobjective_c)
#
# AM_CCASFLAGS = \
# -I$(top_builddir)	\
# -I$(top_srcdir)
#
# ]
#
# #
# # test programs, not to be built by default and never installed
# #
#
# TESTS = test-cpu-accel
#
# test_cpu_accel_SOURCES = test-cpu-accel.c
#
# test_cpu_accel_DEPENDENCIES = \
# 	$(top_builddir)/libgimpbase/libgimpbase-$(GIMP_API_VERSION).la
#
# test_cpu_accel_LDADD = \
# 	$(GLIB_LIBS)	\
# 	$(test_cpu_accel_DEPENDENCIES)
#
#
# EXTRA_PROGRAMS = test-cpu-accel
#
#
# #
# # rules to generate built sources
# #
#
# gen_sources = xgen-bec xgen-cec
# CLEANFILES = $(EXTRA_PROGRAMS) $(gen_sources)
#
# xgen-bec: $(srcdir)/gimpbaseenums.h $(GIMP_MKENUMS) Makefile.am
# 	$(AM_V_GEN) $(GIMP_MKENUMS) \
# 		--fhead "#include \"config.h\"\n#include <glib-object.h>\n#undef GIMP_DISABLE_DEPRECATED\n#include \"gimpbasetypes.h\"\n#include \"libgimp/libgimp-intl.h\"" \
# 		--fprod "\n/* enumerations from \"@basename@\" */" \
# 		--vhead "GType\n@enum_name@_get_type (void)\n{\n  static const G@Type@Value values[] =\n  {" \
# 		--vprod "    { @VALUENAME@, \"@VALUENAME@\", \"@valuenick@\" }," \
# 		--vtail "    { 0, NULL, NULL }\n  };\n" \
# 		--dhead "  static const Gimp@Type@Desc descs[] =\n  {" \
# 		--dprod "    { @VALUENAME@, @valuedesc@, @valuehelp@ }," \
# 		--dtail "    { 0, NULL, NULL }\n  };\n\n  static GType type = 0;\n\n  if (G_UNLIKELY (! type))\n    {\n      type = g_@type@_register_static (\"@EnumName@\", values);\n      gimp_type_set_translation_domain (type, GETTEXT_PACKAGE \"-libgimp\");\n      gimp_type_set_translation_context (type, \"@enumnick@\");\n      gimp_@type@_set_value_descriptions (type, descs);\n    }\n\n  return type;\n}\n" \
# 		$< > $@
#
# # copy the generated enum file back to the source directory only if it's
# # changed; otherwise, only update its timestamp, so that the recipe isn't
# # executed again on the next build, however, allow this to (harmlessly) fail,
# # to support building from a read-only source tree.
# $(srcdir)/gimpbaseenums.c: xgen-bec
# 	$(AM_V_GEN) if ! cmp -s $< $@; then \
# 		cp $< $@; \
# 	else \
# 		touch $@ 2> /dev/null \
# 		|| true; \
# 	fi
#
# xgen-cec: $(srcdir)/gimpcompatenums.h $(GIMP_MKENUMS) Makefile.am
# 	$(AM_V_GEN) $(GIMP_MKENUMS) \
# 		--fhead "#include \"config.h\"\n#include <glib-object.h>\n#include \"gimpbasetypes.h\"\n#include \"gimpcompatenums.h\"\n#include \"libgimp/libgimp-intl.h\"" \
# 		--fprod "\n/* enumerations from \"@basename@\" */" \
# 		--vhead "GType\n@enum_name@_get_type (void)\n{\n  static const G@Type@Value values[] =\n  {" \
# 		--vprod "    { @VALUENAME@, \"@VALUENAME@\", \"@valuenick@\" }," \
# 		--vtail "    { 0, NULL, NULL }\n  };\n" \
# 		--dhead "  static const Gimp@Type@Desc descs[] =\n  {" \
# 		--dprod "    { @VALUENAME@, @valuedesc@, @valuehelp@ }," \
# 		--dtail "    { 0, NULL, NULL }\n  };\n\n  static GType type = 0;\n\n  if (G_UNLIKELY (! type))\n    {\n      type = g_@type@_register_static (\"@EnumName@\", values);\n      gimp_type_set_translation_domain (type, GETTEXT_PACKAGE \"-libgimp\");\n      gimp_type_set_translation_context (type, \"@enumnick@\");\n      gimp_@type@_set_value_descriptions (type, descs);\n    }\n\n  return type;\n}\n" \
# 		$< > $@
#
# # copy the generated enum file back to the source directory only if it's
# # changed; otherwise, only update its timestamp, so that the recipe isn't
# # executed again on the next build, however, allow this to (harmlessly) fail,
# # to support building from a read-only source tree.
# $(srcdir)/gimpcompatenums.c: xgen-cec
# 	$(AM_V_GEN) if ! cmp -s $< $@; then \
# 		cp $< $@; \
# 	else \
# 		touch $@ 2> /dev/null \
# 		|| true; \
# 	fi
#
# DISTCLEANFILES = gimpversion.h








libgimpbase_sources = [
  'gimpbase-private.c',
  'gimpbaseenums.c',
  'gimpbasetypes.c',
  'gimpchecks.c',
  'gimpcompatenums.c',
  'gimpcpuaccel.c',
  'gimpdatafiles.c',
  'gimpenv.c',
  'gimpmemsize.c',
  'gimpmetadata.c',
  'gimpparasite.c',
  'gimpparasiteio.c',
  'gimpprotocol.c',
  'gimprectangle.c',
  'gimpreloc.c',
  'gimpsignal.c',
  'gimpunit.c',
  'gimputils.c',
  'gimpvaluearray.c',
  'gimpwire.c',
  'test-cpu-accel.c',
]

libgimpbase_sources += [
  'gimpbaseenums.c',
  'gimpcompatenums.c',
]

libgimpbase_headers = [
  'gimpbase.h',
  'gimpbaseenums.h',
  'gimpbasetypes.h',
  'gimpcpuaccel.h',
  'gimplimits.h',
  'gimpparam.h',
  'gimpversion.h',
  'gimpchecks.h',
  'gimpdatafiles.h',
  'gimpenv.h',
  'gimpmemsize.h',
  'gimpmetadata.h',
  'gimpparasite.h',
  'gimpparasiteio.h',
  'gimprectangle.h',
  'gimpsignal.h',
  'gimpunit.h',
  'gimputils.h',
  'gimpvaluearray.h',
]




libgimpbase = library('gimpbase-' + api_version,
  libgimpbase_sources,

  include_directories: rootInclude,
  dependencies: [
    gio, gexiv2,
  ],
  c_args: global_cflags,
  link_args: global_lflags,
)
