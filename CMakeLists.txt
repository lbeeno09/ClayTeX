cmake_minimum_required(VERSION 3.10)
set(PROJECT_NAME cLayTeX)
project(${PROJECT_NAME} VERSION 1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED On)

# Variables
set(DEPS_DIR "${CMAKE_SOURCE_DIR}/deps")
# setup vcpkg toolchain
if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
	set(
		CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
		CACHE STRING "Vcpkg toolchain file"
	)
endif()
set(VCPKG_MANIFEST_MODE ON)

# link libraries from vcpkg
#find_package({pkg} CONFIG REQUIRED)

# add submodules from submodules
#add_subdirectory(deps/{submodules})

# add manually added libraries
#add_library({manual} STATIC IMPORTED)
#set_target_properties({manual} PROPERTIES
	#IMPORTED_LOCATION "${DEPS_DIR}/{manual}/lib.lib"
	#INTERFACE_INCLUDE_DIRECTORIES "${DEPS_DIR}/manual/include"
#)

# directories for main project
include_directories(${CMAKE_SOURCE_DIR}/include)
file(GLOB_RECURSE SOURCES ${CMAKE_SOURCE_DIR}/src/*.cpp)


add_executable(${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME} PRIVATE
	# vcpkg/submodule libraries goes here
	#{pkg}::{pkg}
	#{submodules}
	#{manual}
)
