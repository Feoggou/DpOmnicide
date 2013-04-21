include_directories(Dependencies/Recast/Detour/include)
include_directories(Dependencies/Recast/Recast/include)
include_directories(Dependencies/SDL/include)
include_directories(Dependencies/SDL64/include)

include_directories(Dependencies/cap)
include_directories(Dependencies/cd)
include_directories(Dependencies/cl)
include_directories(Dependencies/clvm)
include_directories(Dependencies/gl)
include_directories(Dependencies/mod)
include_directories(Dependencies/model)
include_directories(Dependencies/prvm)
include_directories(Dependencies/r)
include_directories(Dependencies/shader)
include_directories(Dependencies/snd)
include_directories(Dependencies/sv)
include_directories(Dependencies/svvm)
include_directories(Dependencies/sys)
include_directories(Dependencies/thread)
include_directories(Dependencies/vid)

set(current_dir ${darkplaces_SOURCE_DIR}/darkplaces)
message("current dir: ${current_dir}")

link_directories(${current_dir}/Dependencies/SDL/lib)
link_directories(${current_dir}/Dependencies/SDL64/lib)

# file(GLOB c_sources 	*.c)
file(GLOB cpp_sources	*.cpp)
file(GLOB h_headers		*.h)

macro(RemoveFile file_list)
    foreach(file_item ${ARGN})
		set(file_item ${current_dir}/${file_item})
        if(${file_list})
            list(REMOVE_ITEM ${file_list} ${file_item} ${file_item}.cpp ${file_item}.c ${file_item}.h)
			# set(x, get_filename_component(${file_item} ABSOLUTE))
			# message("full name: ${x}")
			message("excluding item: ${file_item}")
        endif()
    endforeach()
endmacro()

# message(c_sources)

source_group("Code" FILES ${cpp_sources} ${h_headers})

file(GLOB cpp_sources_cap	cap/*.cpp)
file(GLOB h_headers_cap		cap/*.h)

source_group("cap" FILES ${cpp_sources_cap} ${h_headers_cap})

file(GLOB cpp_sources_cd	cd/*.cpp)
file(GLOB h_headers_cd		cd/*.h)

source_group("cd" FILES ${cpp_sources_cd} ${h_headers_cd})

file(GLOB cpp_sources_cl	cl/*.cpp)
file(GLOB h_headers_cl		cl/*.h)

source_group("cl" FILES ${cpp_sources_cl} ${h_headers_cl})

file(GLOB cpp_sources_clvm	clvm/*.cpp)
file(GLOB h_headers_clvm		clvm/*.h)

source_group("clvm" FILES ${cpp_sources_clvm} ${h_headers_clvm})

file(GLOB cpp_sources_gl	gl/*.cpp)
file(GLOB h_headers_gl		gl/*.h)

source_group("gl" FILES ${cpp_sources_gl} ${h_headers_gl})

file(GLOB cpp_sources_mod	mod/*.cpp)
file(GLOB h_headers_mod		mod/*.h)

source_group("mod" FILES ${cpp_sources_mod} ${h_headers_mod})

file(GLOB cpp_sources_model	model/*.cpp)
file(GLOB h_headers_model		model/*.h)

source_group("model" FILES ${cpp_sources_model} ${h_headers_model})

file(GLOB cpp_sources_prvm	prvm/*.cpp)
file(GLOB h_headers_prvm		prvm/*.h)

source_group("prvm" FILES ${cpp_sources_prvm} ${h_headers_prvm})

file(GLOB cpp_sources_r	r/*.cpp)
file(GLOB h_headers_r		r/*.h)

source_group("r" FILES ${cpp_sources_r} ${h_headers_r})

file(GLOB cpp_sources_shader	shader/*.cpp)
file(GLOB h_headers_shader		shader/*.h)

source_group("shader" FILES ${cpp_sources_shader} ${h_headers_shader})

file(GLOB cpp_sources_snd	snd/*.cpp)
file(GLOB h_headers_snd		snd/*.h)

source_group("snd" FILES ${cpp_sources_snd} ${h_headers_snd})

file(GLOB cpp_sources_sv	sv/*.cpp)
file(GLOB h_headers_sv		sv/*.h)

source_group("sv" FILES ${cpp_sources_sv} ${h_headers_sv})

file(GLOB cpp_sources_svvm	svvm/*.cpp)
file(GLOB h_headers_svvm		svvm/*.h)

source_group("svvm" FILES ${cpp_sources_svvm} ${h_headers_svvm})

file(GLOB cpp_sources_sys	sys/*.cpp)
file(GLOB h_headers_sys		sys/*.h)

source_group("sys" FILES ${cpp_sources_sys} ${h_headers_sys})

file(GLOB cpp_sources_thread	thread/*.cpp)
file(GLOB h_headers_thread		thread/*.h)

source_group("thread" FILES ${cpp_sources_thread} ${h_headers_thread})

file(GLOB cpp_sources_vid	vid/*.cpp)
file(GLOB h_headers_vid		vid/*.h)

source_group("vid" FILES ${cpp_sources_vid} ${h_headers_vid})

if (NOT LINUX)
	# RemoveFile(cpp_sources "cd_bsd.cpp" "cd_linux.cpp" "snd_bsd.cpp" "snd_coreaudio.cpp" "snd_oss.cpp" "thread_pthread.cpp" "sys_linux")
	RemoveFile(cpp_sources_cd "cd/bsd.cpp" "cd/linux.cpp")
	RemoveFile(cpp_sources_snd "snd/bsd.cpp" "snd/coreaudio.cpp" "snd/oss.cpp")
	RemoveFile(cpp_sources_thread "thread/pthread.cpp")
	RemoveFile(cpp_sources_sys "sys/linux")
endif()

# RemoveFile(cpp_sources "cl_video_jamdecode.cpp" "cl_video_libavw.cpp" "crypto-keygen-standalone.cpp" "keysym2ucs.cpp" "snd_3dras.cpp" "snd_alsa.cpp" "vid_agl.cpp" "vid_glx.cpp")

RemoveFile(cpp_sources "crypto-keygen-standalone.cpp" "keysym2ucs.cpp")
RemoveFile(cpp_sources_cl "cl/video_jamdecode.cpp" "cl/video_libavw.cpp")
RemoveFile(cpp_sources_snd "snd/3dras.cpp" "snd/alsa.cpp" "snd/null.cpp" "snd/win.cpp")
RemoveFile(cpp_sources_vid "vid/agl.cpp" "vid/glx.cpp" "vid/wgl.cpp"  "vid/null.cpp")
RemoveFile(cpp_sources_cd "cd/null.cpp" "cd/win.cpp")
RemoveFile(cpp_sources_sys  "sys/win.cpp")
RemoveFile(cpp_sources_thread  "thread/win.cpp" "thread/null.cpp")
RemoveFile(h_headers_snd "snd/3dras.h")

add_executable(omnicide ${cpp_sources} ${h_headers}
${cpp_sources_cap} ${h_headers_cap}
${cpp_sources_cd} ${h_headers_cd}
${cpp_sources_cl} ${h_headers_cl}
${cpp_sources_clvm} ${h_headers_clvm}
${cpp_sources_gl} ${h_headers_gl}
${cpp_sources_mod} ${h_headers_mod}
${cpp_sources_model} ${h_headers_model}
${cpp_sources_prvm} ${h_headers_prvm}
${cpp_sources_r} ${h_headers_r}
${cpp_sources_shader} ${h_headers_shader}
${cpp_sources_snd} ${h_headers_snd}
${cpp_sources_sv} ${h_headers_sv}
${cpp_sources_svvm} ${h_headers_svvm}
${cpp_sources_sys} ${h_headers_sys}
${cpp_sources_thread} ${h_headers_thread}
${cpp_sources_vid} ${h_headers_vid}
)

target_link_libraries(omnicide SDL.lib SDLmain.lib) 