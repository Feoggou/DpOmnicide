include_directories(Dependencies/Recast/Detour/include)
include_directories(Dependencies/Recast/Recast/include)
include_directories(Dependencies/SDL/include)
include_directories(Dependencies/SDL64/include)

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

if (NOT LINUX)
	RemoveFile(cpp_sources "cd_bsd.cpp" "cd_linux.cpp" "snd_bsd.cpp" "snd_coreaudio.cpp" "snd_oss.cpp" "thread_pthread.cpp" "sys_linux")
endif()

RemoveFile(cpp_sources "cl_video_jamdecode.cpp" "cl_video_libavw.cpp" "crypto-keygen-standalone.cpp" "keysym2ucs.cpp" "snd_3dras.cpp" "snd_alsa.cpp" "vid_agl.cpp" "vid_glx.cpp")

RemoveFile(cpp_sources "cd_null.cpp" "cd_win.cpp" "snd_null.cpp" "snd_win.cpp" "sys_win.cpp" "thread_win.cpp" "vid_wgl.cpp" "thread_null.cpp" "vid_null.cpp")
RemoveFile(h_headers "snd_3dras.h")

# message(c_sources)

source_group("Code" FILES ${c_sources} ${cpp_sources} ${h_headers})

add_executable(omnicide ${c_sources} ${cpp_sources} ${h_headers})

target_link_libraries(omnicide SDL.lib SDLmain.lib) 