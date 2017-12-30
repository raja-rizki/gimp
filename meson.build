# Meson build file

# http://bugzilla.gnome.org/enter_bug.cgi?product=GIMP
project('gimp', ['c', 'cpp'], version : '2.9.7',
  meson_version : '>=0.40.0',
  default_options : [
    'sysconfdir=/etc',
    'localstatedir=/var',
    'sharedstatedir=/var/lib'
  ],
)

conf = configuration_data()

pkgconfig = import('pkgconfig')
i18n      = import('i18n')
gnome     = import('gnome')

cc        = meson.get_compiler('c')
prefix    = get_option('prefix')
buildtype = get_option('buildtype')

profiling = get_option('profiling')
ansi      = get_option('ansi')

################################################################################
# Projects infos

# TODO post-merge : simplify the whole version number handling

prettyname = 'GIMP'
full_name  = 'GNU Image Manipulation Program'

# Making releases on the stable branch:
#   micro_version += 1;
#   interface_age += 1;
#
# For a description of libtool version variables, see:
# devel-docs/libtool-instructions.txt

version = meson.project_version().split('.')
major_version = version[0].to_int()
minor_version = version[1].to_int()
micro_version = version[2].to_int()

# TODO cleanup all this versions mess
interface_age = 0
binary_age = 100 * minor_version + micro_version

lt_current = 100 * minor_version + micro_version - interface_age
lt_revision = interface_age
lt_age = binary_age - interface_age
lt_version_info = '@0@:@1@:@2@'.format(lt_current, lt_revision, lt_age)
lt_current_minus_age = lt_current - lt_age

so_version = '@0@.@1@.@2@'.format(lt_revision, lt_current, lt_current_minus_age)

api_version        = '2.0'
app_version        = '2.9'
data_version       = '2.0'
pkgconfig_version  = '2.0'
plugin_version     = '2.0'
sysconf_version    = '2.0'
tool_version       = '2.0'
user_version       = '2.9'

gimp_command = 'gimp-' + app_version
gimp_api_name = 'gimp-' + api_version
package_string = prettyname + ' ' + meson.project_version()

stable = (minor_version % 2 == 0)
conf.set10('GIMP_UNSTABLE', not stable)

################################################################################
# Host system detection

host_cpu = host_machine.cpu()
message('Architecture: ' + host_cpu)

if   host_cpu.startswith('i') and host_cpu.endswith('86')
  have_x86 = true
  conf.set10('ARCH_X86',    true)
elif host_cpu == 'x86_64'
  have_x86 = true
  conf.set10('ARCH_X86',    true)
  conf.set10('ARCH_X86_64', true)
elif host_cpu == 'ppc' or host_cpu == 'powerpc'
  have_ppc = true
  conf.set10('ARCH_PPC',    true)
elif host_cpu == 'ppc64' or host_cpu == 'powerpc64'
  have_ppc = true
  conf.set10('ARCH_PPC',    true)
  conf.set10('ARCH_PPC64',  true)
else
  error('Unknown host architecture')
endif


host_os = host_machine.system()
message('Host os: ' + host_os)

platform_win32 = (host_os.startswith('mingw') or host_os.startswith('cygwin'))
# Is this native win32
os_win32 = host_os.startswith('mingw')

platform_osx = host_os.startswith('darwin')
conf.set('PLATFORM_OSX',  platform_osx)


################################################################################
# Dependencies
math              = cc.find_library('m')

atk               = dependency('atk',                version: '>=2.2.0')

# babl_minver       = '>=0.1.38'
babl_minver       = '>=0.1.30'
babl              = dependency('babl',               version: babl_minver)

cairo_minver      = '>=1.12.2'
cairo             = dependency('cairo',              version: cairo_minver)

dbus_glib         = dependency('dbus-glib-1')

fontconfig_minver = os_win32 ? '>=2.11.1' : '>=2.2.0'
fontconfig_name   = 'fontconfig' + (os_win32 ? '_win32' : '')
fontconfig        = dependency(fontconfig_name,      version: fontconfig_minver)

freetype2         = dependency('freetype2',          version: '>=2.1.7')

gdk_pixbuf_minver = '>=2.30.8'
gdk_pixbuf        = dependency('gdk-pixbuf-2.0',     version: gdk_pixbuf_minver)

# gegl_minver       = '>=0.3.22'
gegl_minver       = '>=0.3.20'
gegl              = dependency('gegl-0.3',           version: gegl_minver)

gexiv2            = dependency('gexiv2',             version: '>=0.10.6')

gio               = dependency('gio-2.0')
gio_specific_name = 'gio-' + (os_win32 ? 'windows-2.0' : 'unix-2.0')
gio_specific      = dependency(gio_specific_name)

glib              = dependency('glib-2.0',           version: '>=2.43.0')
gobject           = dependency('gobject-2.0',        version: '>=2.43.0')
gmodule           = dependency('gmodule-no-export-2.0')

gtk2_minver       = '>=2.24.10'
gtk2              = dependency('gtk+-2.0',           version: gtk2_minver)

harfbuzz          = dependency('harfbuzz',           version: '>=0.9.19')
lcms              = dependency('lcms2',              version: '>=2.8')
libmypaint        = dependency('libmypaint-1.3',     version: '>=1.3.0')
pangocairo        = dependency('pangocairo',         version: '>=1.29.4')
rsvg              = dependency('librsvg-2.0',        version: '>=2.40.6')

# xgettext           = dependency('xgettext',           version: '>=0.19')

################################################################################
# Check for GLib Networking

have_glib_networking_run = cc.run(
  '''#include <gio/gio.h>
  int main() {
    return !g_tls_backend_supports_tls (g_tls_backend_get_default ());
  }''',
  dependencies: gio,
)
have_glib_networking = (have_glib_networking_run.compiled()
                    and have_glib_networking_run.returncode() == 0)

if not have_glib_networking
  error('Test for glib-networking failed. This is required.')
# TODO check if cross-compiling
endif

################################################################################
# Check if Pango is built with a recent fontconfig

pango_check_run = cc.run(
  '''#include <fontconfig/fontconfig.h>
  int main() {
    FcObjectSet *os; os = FcObjectSetBuild (FC_FAMILY, FC_WIDTH);
  }''',
  dependencies: fontconfig,
)
pango_check =(pango_check_run.compiled()
          and pango_check_run.returncode() == 0)

if not pango_check
  message('''
  *** You have a fontconfig >= fontconfig_required_version installed on your system, but your
  *** Pango library is using an older version. This old version is probably in
  *** /usr/X11R6. Look at the above output, and note that the result for
  *** FONTCONFIG_CFLAGS is not in the result for PANGOCAIRO_CFLAGS, and that
  *** there is likely an extra -I line, other than the ones for GLIB,
  *** Freetype, and Pango itself. That's where your old fontconfig files are.
  *** Rebuild pango, and make sure that it uses the newer fontconfig. The
  *** easiest way be sure of this is to simply get rid of the old fontconfig.
  *** When you rebuild pango, make sure the result for FONTCONFIG_CFLAGS is
  *** the same as the result here.''')
endif

# Check for Dr. Mingw
# TODO check if that works
have_drmingw = false
if platform_win32
  exchndl = cc.find_library('exchndl')
  if exchndl.found()
    have_drmingw = cc.has_function(
      'ExcHndlSetLogFileNameA',
      prefix: '',
      dependencies: exchndl,
    )
  endif
endif

# Check for finite or isfinite
has_finite  = cc.has_function('finite',   prefix: '#include <math.h>')
has_isfinite= cc.has_function('isfinite', prefix: '#include <math.h>')
conf.set('HAVE_FINITE',   has_finite)
conf.set('HAVE_ISFINITE', has_isfinite)

# Check for compiler CPU extensions

has_ssem = cc.has_argument('-mfpmath=sse')
if has_ssem
  add_project_arguments('-mfpmath=sse',
    language: ['c', 'cxx'])
endif

has_mmx  = cc.has_argument('-mmmx') and get_option('enable-mmx')
if has_mmx
  add_project_arguments(   '-mmmx',
    language: ['c', 'cxx'])
endif

has_sse  = cc.has_argument('-msse') and get_option('enable-sse')
if has_sse
  add_project_arguments(   '-msse',
    language: ['c', 'cxx'])
endif

has_sse2 = cc.has_argument('-msse2')
if has_sse2
  add_project_arguments(   '-msse2',
    language: ['c', 'cxx'])
endif

has_sse41= cc.has_argument('-msse4.1')
if has_sse41
  add_project_arguments(   '-msse4.1',
    language: ['c', 'cxx'])
endif

conf.set10('COMPILE_SSE2_INTRINISICS',   has_sse2)
conf.set10('COMPILE_SSE4_1_INTRINISICS', has_sse41)
conf.set10('USE_MMX', has_mmx)
conf.set10('USE_SSE', has_sse)


# TODO altivec
has_altivec = cc.has_argument('-faltivec')
cc.has_argument('-maltivec')
cc.has_argument('-mabi=altivec')


if os_win32
  ole32 = cc.find_library('ole32')
endif


# TODO shared memory handling

# OpenMP
conf.set10('ENABLE_MP', get_option('enable-mp'))

screenshot_deps = []

# Check if X11
enable_doc_shooter = false
have_libxmu = false
have_libxext = false

if gtk2.get_pkgconfig_variable('target') == 'x11'
  enable_doc_shooter = true

  x11 = dependency('x11')

  # Test for Xmu
  xmu = dependency('xmu')
  xt  = dependency('xt')
  if xmu.found() and xt.found()
    if cc.has_header('X11/Xmu/WinUtil.h', dependencies: xmu)
      if cc.has_function('XmuClientWindow', dependencies: xmu)
        have_libxmu = true
        xmu = [ x11, xmu, xt ]
      endif
    endif
  endif

  # Check for shaped window extension
  xext = dependency('xext')
  if xext.found()
    if cc.has_header('X11/extensions/shape.h', dependencies: xext)
      if cc.has_function('XShapeGetRectangles', dependencies: xext)
        have_libxext = true
        xext = [ x11, xext ]
      endif
    endif
  endif

  # check for the XFixes extension
  xfixes = dependency('xfixes')


endif


################################################################################
# MIME types
# The list of MIME types that are supported by plug-ins

MIMEtypes = [
  'image/bmp',
  'image/g3fax',
  'image/gif',
  'image/svg+xml',
  'image/x-compressed-xcf',
  'image/x-fits',
  'image/x-gimp-gbr',
  'image/x-gimp-gih',
  'image/x-gimp-pat',
  'image/x-pcx',
  'image/x-portable-anymap',
  'image/x-portable-bitmap',
  'image/x-portable-graymap',
  'image/x-portable-pixmap',
  'image/x-psd',
  'image/x-sgi',
  'image/x-tga',
  'image/x-xbitmap',
  'image/x-xcf',
  'image/x-xwindowdump',
]


# TIFF support
libtiff = dependency('libtiff-4', required: false)
if libtiff.found()
  MIMEtypes += 'image/tiff'
endif

# Jpeg support
libjpeg = dependency('libjpeg', required: false)
if libjpeg.found()
  MIMEtypes += 'image/jpeg'
endif

# Zlib support
zlib = dependency('zlib', required: false)
if zlib.found()
  MIMEtypes += 'image/x-psp'
endif

# Bz2 support
bz2 = cc.find_library('bz2', required: false)

# LZma support
lzma = dependency('liblzma', version: '>=5.0.0', required: false)

# Ghostscript / Postscript support
have_ghostscript = false
if get_option('with-gs')
  have_ghostscript = true
  ghostscript = cc.find_library('gs')
  MIMEtypes += 'application/postscript'
endif

# LibPNG
libpng = dependency('libpng', version: '>=1.6.25', required: false)
if libpng.found()
  MIMEtypes += [ 'image/png', 'image/x-icon']
endif

# LibMNG
have_libmng = false
if get_option('with-mng')
  have_libmng = true
  libmng = cc.find_library('mng')
endif

# Libaa
have_libaa = false
if get_option('with-aa')
  have_libaa = true
  liba = cc.find_library('aa')
endif


# Libxpm
have_libxpm = false
if get_option('with-xpm')
  have_libxpm = true
  libpng = dependency('xpm')
  MIMEtypes += 'image/x-xpixmap'
endif

# OpenEXR
have_openexr = false
if get_option('with-openexr')
  have_openexr = true
  openexr = dependency('OpenEXR', version: '>=1.6.1')
  MIMEtypes += 'image/x-exr'
endif

# WebP
have_webp = false
if get_option('with-webp')
  have_webp = true
  webp = [
    dependency('libwebp',     version: '>=0.6.0'),
    dependency('libwebpmux',  version: '>=0.6.0'),
    dependency('libwebpdemux',version: '>=0.6.0'),
  ]
  MIMEtypes += 'image/x-webp'
endif


# WebKit
have_webkit = false
if get_option('with-webkit')
  have_webkit = true
  webkit = dependency('webkit-1.0', version: '>=1.6.1')
endif


# poppler
have_poppler = false
if get_option('with-poppler')
  have_poppler = true
  poppler = [
    dependency('poppler-glib', version: '>=0.44.0'),
    dependency('poppler-data', version: '>=0.4.7'),
  ]
endif

# cairo-pdf
have_cairopdf = false
if get_option('with-cairo-pdf')
  have_cairopdf = true
  cairopdf = dependency('cairo-pdf', version: '>=1.12.2')
endif

# If both poppler and cairo-pdf are enabled then we have complete PDF support
if have_poppler and have_cairopdf
  MIMEtypes += 'application/pdf'
endif


# libwmf2
have_wmf = false
if get_option('with-wmf')
  have_wmf = true
  wmf = cc.find_library('wmf')
  wmf_version = run_command('libwmf-config', '--version').stdout().strip()
  if not wmf_version.version_compare('>=0.2.8')
    error('libwmf version is too old (' + wmf_version + ', 0.2.8 required)')
  endif
  MIMEtypes += [ 'image/x-wmf', ]
endif

# libjasper
have_jasper = false
if get_option('with-jasper')
  have_jasper = true
  jasper = cc.find_library('jasper')
  MIMEtypes += [ 'image/jp2', 'image/jpeg2000', 'image/jpx', ]
endif

# xcursor / xmc
have_xmc = false
if get_option('with-xmc')
  have_xmc = true
  xmc = dependency('xcursor')
  MIMEtypes += [ 'image/x-xcursor', ]
endif

# alsa
have_alsa = false
if get_option('with-alsa')
  have_alsa = true
  alsa = dependency('alsa', version: '>=1.0.0')
endif

# Linux-input
have_linuxinput = false
if get_option('with-linux-input')
  if not cc.has_header('linux/input.h')
    error('linux/input.h header not found.')
  endif
  have_linuxinput = true
endif

# DirectX DirectInput
have_directXinput = false
directx_sdk_path = get_option('with-directx-sdk')
if directx_sdk_path != '' and os_win32
  if directx_sdk_path.contains(' ')
    message('Warning: The DirectX SDK should be accessible through a path without spaces. Use MSYS mounts.'
        + '\nIgnoring your with-directx-sdk switch.'
    )
  elif directx_sdk_path.contains('\\')
    message('Warning: Use plain (forward) slashes only for the DirectX SDK path.'
        + '\nIgnoring your with-directx-sdk switch.'
    )
  else
    have_directXinput = true
    conf.set10('HAVE_DX_DINPUT', have_directXinput)
    dxguid = cc.find_library('dxguid',
      dirs: join_paths(directx_sdk_path, 'Lib', 'x86'),
    )
    directx = declare_dependency(link_with: dxguid,
      include_directories: join_paths(directx_sdk_path, 'Include'),
    )
  endif
endif


# libgudev
have_gudev = false
if get_option('with-gudev')
  have_gudev = true
  gudev = dependency('gudev-1.0',version: '>=167')
endif


# sendmail TODO
have_email = true
# have_gudev = false
# if get_option('with-gudev')
#   have_gudev = true
#   gudev = dependency('gudev-1.0',version: '>=167')
# endif

# perl
perl = find_program('perl5', 'perl', 'perl5.005', 'perl5.004', 'perl')


# python
have_python = false
if get_option('with-python')
  python2 = find_program('python2')
  pygtk2codegen = find_program('pygtk-codegen-2.0')

  libpy2  = dependency('python2',   version: '>=2.5.0')
  pygtk2  = dependency('pygtk-2.0', version: '>=2.10.4')
  pycairo = dependency('pycairo',   version: '>=1.0.2')

  pygtk_defsdir = pygtk2.get_pkgconfig_variable('defsdir')
  have_python = true
endif


# Script-fu
have_scriptfu = get_option('with-script-fu')


# Print support
have_print = get_option('with-print')


# Check for GTK Mac Integration
gtk_mac_integration_ok = false
if platform_osx and (gtk2.get_pkgconfig_variable('target') == 'xquartz')
  gtk2_macos   = dependency('gtk-mac-integration-gtk2', version: '>=2.0.0', required: false)
  if not gtk2_macos.found()
    gtk2_macos = dependency('gtk-mac-integration'     , version: '>=2.0.0', required: false)
  endif
  gtk_mac_integration_ok = gtk2_macos.found()
endif

# Check for XML tools
xmllint = find_program('xmllint', required: false)
xsltproc= find_program('xsltproc',required: false)
intltool_merge = find_program('intltool-merge')
desktop_validate = find_program('desktop-file-validate')
gdk_pixbuf_csource = find_program('gdk-pixbuf-csource')


# Check for vector icons
# TODO
have_vector_icons = true
# if get_option('with-vec-icons')
#   # shared-mime-info is needed to correctly detect SVG files
#   # (except on Windows, apparently).
#   shared_mime_info = dependency('shared-mime-info', required: false)
#   if shared_mime_info.found() or platform_win32
#
#   endif
# endif

# Check for xvfb-run
have_xvfb_run = false
if get_option('with-xvfb-run')
  xvfb_run = find_program('xvfb-run')
  have_xvfb_run = true
endif


# Check for appstream-util
have_appstream_util = false
if get_option('with-appdata-test')
  appstream_util = find_program('appstream-util')
  have_appstream_util = true
endif


# Check for gtk-doc and docbook-tools
have_gtk_doc = false
if get_option('with-gtk-doc')
  gtk_doc_scan = find_program('gtkdoc-scan', required : true)
  have_gtk_doc = true
endif

enable_default_bin = get_option('enable-default-bin')
enable_console_bin = get_option('enable-console-bin')


# Possibly change default gimpdir from $XDG_CONFIG_HOME/GIMP/gimp_user_version
gimpdir = get_option('gimpdir')
if gimpdir == ''
  # Default value
  gimpdir = meson.project_name()
endif

gimpdatadir    = join_paths(get_option('datadir'),    meson.project_name(), data_version)
gimpplugindir  = join_paths(get_option('libdir'),     meson.project_name(), plugin_version)
gimpsysconfdir = join_paths(get_option('sysconfdir'), meson.project_name(), sysconf_version)
gimpmanpagedir = gimpdir
localedir  = join_paths(get_option('datadir'), 'locale')



# Disable deprecated APIs
add_project_arguments([
  '-DGIMP_DISABLE_DEPRECATED',
  '-DBABL_DISABLE_DEPRECATED',
  '-DGSEAL_ENABLE'
  ],
  language: 'c',
)

if glib.version().version_compare('>=2.43')
  add_project_arguments([
    '-DG_DISABLE_DEPRECATED',
    ],
    language: 'c',
  )
endif
if gtk2.version().version_compare('>=2.26')
  add_project_arguments([
    '-DGDK_DISABLE_DEPRECATED',
    '-DGTK_DISABLE_DEPRECATED',
    ],
    language: 'c',
  )
endif
if glib.version().version_compare('>=1.32')
  add_project_arguments([
    '-DPANGO_DISABLE_DEPRECATED',
    ],
    language: 'c',
  )
endif


# Require multihead safe API
add_project_arguments([
  '-DGDK_MULTIHEAD_SAFE',
  '-DGTK_MULTIHEAD_SAFE',
  ],
  language: 'c',
)


# Check for internal tools
defcheck            = find_program(join_paths('tools', 'defcheck.py'))
extract_vector_icon = find_program(join_paths('tools', 'extract-vector-icon.sh'))
generate_changelog  = find_program(join_paths('tools', 'generate_changelog.sh'))
generate_news       = find_program(join_paths('tools', 'generate-news'))
gimppath2svg        = find_program(join_paths('tools', 'gimppath2svg.py'))
module_dependencies = find_program(join_paths('tools', 'module-dependencies.py'))

gimp_mkenums        = find_program(join_paths('tools', 'gimp-mkenums'))
gimp_mkenums_custom_target_commonargs = [
  '--fprod','/* enumerations from "@basename@" */\n',
  '--vhead','GType\n'+
            '@enum_name@_get_type (void)\n'+
            '{\n'+
            '  static const G@Type@Value values[] =\n'+
            '  {',
  '--vprod','    { @VALUENAME@, "@VALUENAME@", "@valuenick@" },',
  '--vtail','    { 0, NULL, NULL }\n'+
            '  };\n',
  '--dhead','  static const Gimp@Type@Desc descs[] =\n'+
            '  {',
  '--dprod','    { @VALUENAME@, @valuedesc@, @valuehelp@ },',
  '--dtail','    { 0, NULL, NULL }\n'+
            '  };\n'+
            '\n'+
            '  static GType type = 0;\n'+
            '\n'+
            '  if (G_UNLIKELY (! type))\n'+
            '    {\n'+
            '      type = g_@type@_register_static ("@EnumName@", values);\n'+
            '      gimp_type_set_translation_context (type, "@enumnick@");\n'+
            '      gimp_@type@_set_value_descriptions (type, descs);\n'+
            '    }\n'+
            '\n'+
            '  return type;\n'+
            '}\n',
  '@INPUT@',
]


################################################################################
# Localisation
gettext_package = 'gimp20'

conf.set_quoted('GETTEXT_PACKAGE',gettext_package)

# localedir = join_paths(get_option('prefix'), get_option('localedir'))


################################################################################
# ISO codes

isocodes = dependency('iso-codes', required: false)
if isocodes.found()
  isocodes_prefix = isocodes.get_pkgconfig_variable('prefix')
  isocodes_location = join_paths(isocodes_prefix,get_option('datadir'),'xml','iso-codes')
  isocodes_localedir= join_paths(isocodes_prefix,get_option('datadir'),'locale')
endif


################################################################################
# CFlags

if profiling
  add_project_arguments('-pg', language: 'c')
endif

if ansi
  add_project_arguments('-ansi', '-pedantic', language: 'c')
endif

add_project_arguments(
  '-fdiagnostics-show-option',
  '-fno-common',

  '-Wmissing-prototypes',
  '-Werror=missing-prototypes',

  '-Wdeclaration-after-statement',
  '-Wformat-security',
  '-Winit-self',
  '-Wlogical-op',
  '-Wmissing-declarations',
  '-Wmissing-format-attribute',
  '-Wold-style-definition',
  '-Wpointer-arith',
  '-Wreturn-type',
  # '-Wstrict-prototypes',
  '-Wtype-limits',

  # '--omg-optimized',
  # '--disable-instructions',
  language: 'c'
)

# Ensure MSVC-compatible struct packing convention is used when
# compiling for Win32 with gcc.
if os_win32
  add_project_arguments(
    cc.first_supported_argument('-fnative-struct', '-mms-bitfields')
	)
endif

has_nl_measurement = cc.has_function(
  'nl_langinfo',
  prefix: '#include<langinfo.h>',
)

################################################################################
# Set/regroup common CFlags for subdirs

libgimp_cflags = [
  '-DPREFIX="'+ prefix + '"',
  '-DGIMPDIR="'+ gimpdir + '"',
  '-DPACKAGE_STRING="'+ package_string + '"',
  '-DDATADIR="'+ gimpdatadir + '"',
  '-DLOCALEDIR="'+ localedir + '"',
  '-DPLUGINDIR="'+ gimpplugindir + '"',
  '-DSYSCONFDIR="'+ gimpsysconfdir + '"',
  '-DGIMP_PACKAGE="'+ meson.project_name() + '"',
  '-DGIMP_DATA_VERSION="'+ data_version + '"',
  '-DGIMP_USER_VERSION="'+ user_version + '"',
  '-DGIMP_SYSCONF_VERSION="'+ sysconf_version + '"',
  '-DGIMP_PLUGIN_VERSION="'+ plugin_version + '"',
]
libgimp_lflags = []

if platform_win32
  libgimp_cflags += '-no-undefined'
endif

if platform_osx
  libgimp_cflags += '-xobjective-c'
  libgimp_lflags += ['-framework', 'Cocoa']
endif

rootInclude = include_directories('.')

################################################################################
# Subdirs

# Tools (need libgimpbase now)
subdir('libgimpbase')
subdir('tools')

# Translations
subdir('po')
subdir('po-libgimp')
subdir('po-plug-ins')
subdir('po-python')
subdir('po-script-fu')
subdir('po-tags')
subdir('po-tips')

# Data / Desktop / xml files
subdir('cursors')
subdir('data')
subdir('desktop')
subdir('etc')
subdir('icons')
subdir('m4macros')
subdir('menus')
subdir('themes')

# Docs
subdir('devel-docs')
subdir('docs')

# Libraries (order here is important!)
subdir('libgimpcolor')
subdir('libgimpmath')
subdir('libgimpconfig')
subdir('libgimpmodule')
subdir('libgimpthumb')
subdir('libgimpwidgets')
subdir('libgimp')

# Executables, plugins
subdir('modules')
# subdir('plug-ins')
subdir('app')

subdir('tools/pdbgen')

# subdir('build')
# build/windows/gimp-plug-ins.rc
# build/windows/gimp.rc



# configure_file(
#   input : 'INSTALL.in',
#   output: 'INSTALL',
#   configuration: conf
# )

configure_file(
  output: 'config.h',
  configuration: conf
)


# TODO sysconfdir seems not correctly set
pkgconfig.generate(filebase: 'gimp-' + pkgconfig_version,
  name: prettyname,
  description: 'GIMP Library',
  version: meson.project_version(),
  requires: [
    'gdk-pixbuf-2.0 ' + gdk_pixbuf_minver,
    'cairo '          + cairo_minver,
    'gegl-0.3 '       + gegl_minver,
  ],
  libraries: [
    '-L${libdir}',
    '-lgimp-'       + api_version,
    '-lgimpmath-'   + api_version,
    '-lgimpconfig-' + api_version,
    '-lgimpcolor-'  + api_version,
    '-lgimpbase-'   + api_version,
  ],
  subdirs: [
    gimp_api_name,
  ],
  variables: [
    'gimpdatadir=' + gimpdatadir,
    'gimplibdir=' + gimpplugindir,
    'gimpsysconfdir=' + gimpsysconfdir,
    'gimplocaledir=' + localedir,
  ],
)
pkgconfig.generate(filebase: 'gimpthumb-' + pkgconfig_version,
  name: 'GIMP Thumb',
  description: 'GIMP Thumbnail Library',
  version: meson.project_version(),
  requires: [
    'gdk-pixbuf-2.0 ' + gdk_pixbuf_minver,
  ],
  libraries: [
    '-L${libdir}',
    '-lgimpthumb-'  + api_version,
  ],
  subdirs: [
    gimp_api_name,
  ],
)
pkgconfig.generate(filebase: 'gimpui-' + pkgconfig_version,
  name: 'GIMP UI',
  description: 'GIMP User Interface Library',
  version: meson.project_version(),
  requires: [
    'gimp-' + pkgconfig_version + ' >= ' + app_version,
    'gtk+-2.0 ' + gtk2_minver,
  ],
  libraries: [
    '-L${libdir}',
    '-lgimpui-'  + api_version,
    '-lgimpwidgets-' + api_version,
    '-lgimpmodule-'  + api_version,
  ],
  subdirs: [
    gimp_api_name,
  ],
)


# Print a summary of features enabled/disabled:

message('''
Extra Binaries:
  gimp-console:        @0@'''.format(enable_console_bin) +'''

Optional Features:
  Language selection:  @0@'''.format(isocodes.found()) +'''
  Vector icons:        @0@'''.format(have_vector_icons) +'''
  Dr. Mingw (Win32):   @0@'''.format(have_drmingw) +'''

Optional Plug-Ins:
  Ascii Art:           @0@'''.format(have_libaa) +'''
  Ghostscript:         @0@'''.format(have_ghostscript) +'''
  Help Browser:        @0@'''.format(have_webkit) +'''
  JPEG 2000:           @0@'''.format(have_jasper) +'''
  MNG:                 @0@'''.format(have_libmng) +'''
  OpenEXR:             @0@'''.format(have_openexr) +'''
  WebP:                @0@'''.format(have_webp) +'''
  PDF (import):        @0@'''.format(have_poppler) +'''
  PDF (export):        @0@'''.format(have_cairopdf) +'''
  Print:               @0@'''.format(have_print) +'''
  Python 2:            @0@'''.format(have_python) +'''
  Script-Fu:           @0@'''.format(have_scriptfu) +'''
  TWAIN (Win32):       @0@'''.format(os_win32) +'''
  Webpage:             @0@'''.format(have_webkit) +'''
  WMF:                 @0@'''.format(have_wmf) +'''
  X11 Mouse Cursor:    @0@'''.format(have_xmc) +'''
  XPM:                 @0@'''.format(have_libxpm) +'''
  Email:               @0@'''.format(have_email) +'''

Optional Modules:
  ALSA (MIDI Input):   @0@'''.format(have_alsa) +'''
  Linux Input:         @0@'''.format(have_linuxinput) +''' (GUdev support: @0@'''.format(have_gudev) +''')
  DirectInput (Win32): @0@'''.format(have_directXinput) +'''

Tests:
  Use xvfb-run         @0@'''.format(have_xvfb_run) +'''
  Test appdata         @0@'''.format(have_appstream_util) +'''
'''
)


# Miscelaneous targets

if xsltproc.found()
  custom_target('AUTHORS',
    input : [ 'authors.xsl', 'authors.xml', ],
    output: 'AUTHORS',
    command: [
      xsltproc.path(),
      '-o', '@OUTPUT@',
      '@INPUT@',
    ],
    build_by_default: false,
  )
  custom_target('authors.md',
    input : [ 'authors4gimp-web.xsl', 'authors.xml', ],
    output: 'authors.md',
    command: [
      xsltproc.path(),
      '--stringparam', 'today', '`date --iso-8601=seconds`',
      '-o', '@OUTPUT@',
      '@INPUT@',
    ],
    build_by_default: false,
  )
endif

if xmllint.found()
  custom_target('validate-authors',
    input : [ 'authors.xml', ],
    output: [ 'validate-authors', ],
    command: [
      xmllint.path(),
      '--noout',
      '--valid', '@INPUT@',
    ],
    build_by_default: false,
  )
endif

# TODO this python script is waiting for autotools directory/files structure
custom_target('check-defs',
  input : [ ],
  output: [ 'check-defs', ],
  command: [
    python2.path(),
    join_paths(meson.source_root(), 'tools','defcheck.py'),
    meson.source_root(),
  ],
  build_by_default: false,
)


custom_target('Changelog',
  input : [ ],
  output: [ 'Changelog', ],
  command: [
    join_paths(meson.source_root(), 'tools','generate_changelog.sh'),
    meson.source_root(),
    '@OUTPUT@'
  ],
  build_by_default: false,
)
