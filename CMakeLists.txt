cmake_minimum_required(VERSION 3.4.1)

project(Opusfile)

if( ANDROID )
	set(CMAKE_CXX_FLAGS_DEBUG "-g3 -O0")
	set(CMAKE_C_FLAGS_DEBUG "-g3 -O0")
	set(CMAKE_CXX_FLAGS_RELEASE "-O2 -s -DNDEBUG")
	set(CMAKE_C_FLAGS_RELEASE "-O2 -s -DNDEBUG")
	set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "-g3 -Og")
	set(CMAKE_C_FLAGS_RELWITHDEBINFO "-g3 -Og")
	set(CMAKE_CXX_FLAGS_MINSIZEREL "-Os -s -DNDEBUG")
	set(CMAKE_C_FLAGS_MINSIZEREL "-Os -s -DNDEBUG")
endif()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")

include_directories( . include ../libogg/include ../opus/include )

add_definitions(-DOP_FIXED_POINT)


add_library( opusfile_static STATIC
src/http.c
src/info.c
src/internal.c
src/opusfile.c
src/stream.c
src/wincerts.c 
)

add_library(opusfile SHARED
src/http.c
src/info.c
src/internal.c
src/opusfile.c
src/stream.c
src/wincerts.c
)

# 指定静态库的输出名称
set_target_properties(opusfile_static PROPERTIES OUTPUT_NAME "opusfile")
# 使动态库和静态库同时存在
set_target_properties(opusfile PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(opusfile_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)


