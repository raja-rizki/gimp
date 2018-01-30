if platform_win32

# Win32 specific
plugin_twain_sources = [
  'tw_func.c',
  'tw_util.c',
  'tw_win.c',
  'twain.c',
]
# if HAVE_WINDRES
#   GIMPPLUGINRC = $(top_builddir)/build/windows/gimp-plug-ins.rc
#
#   # `windres` seems a very stupid tool and it breaks with double shlashes
#   # in parameter paths. Strengthen the rule a little.
#
#   twain_rc_name = 'twain.rc'
#   twain_rc = custom_target(twain_rc_name + '.o',
#     input : [],
#     output: [ twain_rc_name + '.o', ],
#     command: [
#       '$(WINDRES)',
#       '--define', 'ORIGINALFILENAME_STR="$*$(EXEEXT)"'
#       '--define', 'INTERNALNAME_STR="$*"'
#       '--define', 'TOP_SRCDIR="`echo $(top_srcdir) | sed 's*//*/*'`"'
#       '-I"`echo', '$(top_srcdir)/app | sed 's%/\+%/%'`"'
#       '-I"`echo', '$(top_builddir)/app | sed 's%/\+%/%'`"'
#       '$(GIMPPLUGINRC) $@
#     ],
#   )
#
# endif

twain = executable('twain',
  plugin_twain_sources,
  include_directories: [ rootInclude, ],
  dependencies: [
    glib, gtk2, gegl,
  ],
  link_with: [
    libgimp,
    libgimpcolor,
    libgimpbase,
  ],
  install: true,
  install_dir: join_paths(gimpplugindir, 'plug-ins'),
)

endif
