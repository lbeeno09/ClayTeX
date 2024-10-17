cmake_minimum_required(VERSION 3.10)
set(PROJECT_NAME cLayTeX)
project(${PROJECT_NAME} VERSION 1.0)

# Variables
set(DEPS_DIR "${CMAKE_SOURCE_DIR}/deps")
# setup vcpkg toolchain
if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
	set(
		CMAKE_TOOLCHAIN_FILE "${DEPS_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
		CACHE STRING "Vcpkg toolchain file"
	)
endif()

# directories for main project
include_directories(${CMAKE_SOURCE_DIR}/include)
file(GLOB_RECURSE SOURCES ${CMAKE_SOURCE_DIR}/src)

# add submodules from submodules
#add_subdirectory(deps/***)

add_executable(${PROJECT_NAME} ${SOURCES})

# link libraries from vcpkg
#find_package(*** CONFIG REQUIRED)

target_link_libraries(${PROJECT_NAME} PRIVATE
	# vcpkg/submodule libraries goes here
)