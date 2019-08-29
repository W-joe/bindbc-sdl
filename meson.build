## Build file for meson

project('bindbc-sdl', 'd',
	meson_version: '>=0.46.0',
	license: 'Boost',
	version: '0.11.0',
	subproject_dir: 'subprojects',
	default_options: [
		'buildtype=release',
		],
	)

compiler_id		= meson.get_compiler('d').get_id()
project_name		= meson.project_name()
project_target		= project_name + '_' + compiler_id
project_description	= 'A dynamic binding to the SDL library.'
project_homepage	= 'https://github.com/BindBC/bindbc-sdl'


## versions
module_versions = []

sdl_version = get_option('sdl_version')
module_versions += sdl_version

sdl_mixer = get_option('sdl_mixer')
module_versions += sdl_mixer

sdl_image = get_option('sdl_image')
module_versions += sdl_image

sdl_ttf = get_option('sdl_ttf')
module_versions += sdl_ttf


## Dependencies
bindbc_loader_dep = dependency('bindbc-loader_' + compiler_id,
	required: false,
	version: '>=0.2.0')

if not bindbc_loader_dep.found()
	bindbc_loader = subproject('bindbc-loader')
	bindbc_loader_dep = bindbc_loader.get_variable('bindbc_loader_dep')
endif


## Import directories
import_dir = include_directories(
	'source/',
	)

## Source Files
source_files = [
	'source/bindbc/sdl/config.d',
	'source/bindbc/sdl/dynload.d',
	'source/bindbc/sdl/image.d',
	'source/bindbc/sdl/mixer.d',
	'source/bindbc/sdl/package.d',
	'source/bindbc/sdl/ttf.d',

	'source/bindbc/sdl/bind/package.d',
	'source/bindbc/sdl/bind/sdlassert.d',
	'source/bindbc/sdl/bind/sdlaudio.d',
	'source/bindbc/sdl/bind/sdlblendmode.d',
	'source/bindbc/sdl/bind/sdlclipboard.d',
	'source/bindbc/sdl/bind/sdlcpuinfo.d',
	'source/bindbc/sdl/bind/sdl.d',
	'source/bindbc/sdl/bind/sdlerror.d',
	'source/bindbc/sdl/bind/sdlevents.d',
	'source/bindbc/sdl/bind/sdlfilesystem.d',
	'source/bindbc/sdl/bind/sdlgamecontroller.d',
	'source/bindbc/sdl/bind/sdlgesture.d',
	'source/bindbc/sdl/bind/sdlhaptic.d',
	'source/bindbc/sdl/bind/sdlhints.d',
	'source/bindbc/sdl/bind/sdljoystick.d',
	'source/bindbc/sdl/bind/sdlkeyboard.d',
	'source/bindbc/sdl/bind/sdlkeycode.d',
	'source/bindbc/sdl/bind/sdlloadso.d',
	'source/bindbc/sdl/bind/sdllog.d',
	'source/bindbc/sdl/bind/sdlmessagebox.d',
	'source/bindbc/sdl/bind/sdlmouse.d',
	'source/bindbc/sdl/bind/sdlpixels.d',
	'source/bindbc/sdl/bind/sdlplatform.d',
	'source/bindbc/sdl/bind/sdlpower.d',
	'source/bindbc/sdl/bind/sdlrect.d',
	'source/bindbc/sdl/bind/sdlrender.d',
	'source/bindbc/sdl/bind/sdlrwops.d',
	'source/bindbc/sdl/bind/sdlscancode.d',
	'source/bindbc/sdl/bind/sdlshape.d',
	'source/bindbc/sdl/bind/sdlstdinc.d',
	'source/bindbc/sdl/bind/sdlsurface.d',
	'source/bindbc/sdl/bind/sdlsystem.d',
	'source/bindbc/sdl/bind/sdlsyswm.d',
	'source/bindbc/sdl/bind/sdltimer.d',
	'source/bindbc/sdl/bind/sdltouch.d',
	'source/bindbc/sdl/bind/sdlversion.d',
	'source/bindbc/sdl/bind/sdlvideo.d',
	'source/bindbc/sdl/bind/sdlvulkan.d',
	]


## Target
target_lib = library(
	project_target,
	sources: source_files,
	include_directories: import_dir,
	dependencies: [bindbc_loader_dep],
	install: true,
	d_module_versions: module_versions,
	pic: true,
	)

install_subdir('source/bindbc/', install_dir: 'include/d/')


## Dependency
bindbc_sdl2_dep = declare_dependency(
	include_directories: import_dir,
	link_with: target_lib,
	version: meson.project_version(),
	dependencies: bindbc_loader_dep,
	)


## pkg-config
pkgConf = import('pkgconfig')
pkgConf.generate(
	name: project_target,
	subdirs: 'd/',
	version: meson.project_version(),
	description: project_description,
	d_module_versions: module_versions,
	libraries: target_lib,
	)

