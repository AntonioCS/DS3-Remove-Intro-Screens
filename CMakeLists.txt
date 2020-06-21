cmake_minimum_required(VERSION 3.15 FATAL_ERROR)
project("Souls Skip Intro Screen" DESCRIPTION "Dll to bypass loading screen of souls games" VERSION 0.0.1 LANGUAGES CXX)
#include(GenerateExportHeader)

set(OUTPUT_FILE dinput8)

if (NOT DEFINED CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 20)
else()
  if (CMAKE_CXX_STANDARD VERSION_LESS 20)
    message(FATAL_ERROR "CMAKE_CXX_STANDARD of 20 or later required.")
  endif()
endif()
if (NOT DEFINED CMAKE_CXX_EXTENSIONS)
  set(CMAKE_CXX_EXTENSIONS OFF)
endif()

if (MSVC)
	add_definitions(-D_UNICODE -DUNICODE -DWIN32_LEAN_AND_MEAN -DNOMINMAX -DWINVER=0x0A00 -D_WIN32_WINNT=0x0A00)
	add_definitions(-D_CRT_SECURE_NO_DEPRECATE -D_CRT_SECURE_NO_WARNINGS -D_CRT_NONSTDC_NO_DEPRECATE)
	add_definitions(-D_ATL_SECURE_NO_DEPRECATE -D_SCL_SECURE_NO_WARNINGS)
endif()
		
file(GLOB_RECURSE PROJ_SRC_FILES
	CONFIGURE_DEPENDS
	src/*.c* src/*.h*
)

#To properly set the files in the treeview for MSVC
foreach(source IN LISTS PROJ_SRC_FILES)
	get_filename_component(source_path "${source}" PATH)
	string(REPLACE "${PROJECT_SOURCE_DIR}/" "" source_path_msvc "${source_path}")
	source_group("${source_path_msvc}" FILES "${source}")
endforeach()

add_library(
	${OUTPUT_FILE} SHARED
	${PROJ_SRC_FILES}
)

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS true)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${OUTPUT_FILE})

#generate_export_header(${OUTPUT_FILE})

target_compile_options(${OUTPUT_FILE}
 PRIVATE
	$<$<OR:$<CXX_COMPILER_ID:Clang>,$<CXX_COMPILER_ID:AppleClang>,$<CXX_COMPILER_ID:GNU>>:
		-Werror -Wall -Wextra>
	$<$<CXX_COMPILER_ID:MSVC>:
		/W4>
)

find_package(minhook CONFIG REQUIRED)
target_link_libraries(${OUTPUT_FILE} PRIVATE minhook::minhook)

