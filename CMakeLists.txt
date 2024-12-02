cmake_minimum_required(VERSION 3.15)

project(tinyhttp CXX)
#option(USE_CLANG "build application with clang" ON) # OFF is the default"")

set(SRC
	http.cpp
	websock.cpp
	)

set(INC
	#${CMAKE_CURRENT_SOURCE_DIR}/include
	#${CMAKE_SOURCE_DIR}/src
	htcc/
	)

add_library(tinyhttp STATIC
	${SRC}
	)

	#target_include_directories(depths-log INTERFACE
	#$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
	#$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/src>
	#)

target_include_directories(tinyhttp PRIVATE
	${INC}
	../MiniJson/Source/include
	)


set_property(TARGET tinyhttp PROPERTY POSITION_INDEPENDENT_CODE ON)
set_property(TARGET tinyhttp PROPERTY CXX_STANDARD 20)

if(MSVC)
else()
target_compile_options(tinyhttp PRIVATE -Wfatal-errors -Werror -Wall -Wextra -Wno-unused-function -Wno-sign-compare -Wno-unused-variable -Wno-switch -Wno-unused-parameter)
endif()
