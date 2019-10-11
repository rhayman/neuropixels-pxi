#plugin build file
cmake_minimum_required(VERSION 3.5.0)

#include common rules
include(../PluginRules.cmake)

#add sources, not including OpenEphysLib.cpp
	add_sources(${PLUGIN_NAME}
	Source/NeuropixComponents.cpp
	Source/NeuropixComponents.h
	Source/NeuropixEditor.cpp
	Source/NeuropixEditor.h
	Source/NeuropixThread.cpp
	Source/NeuropixThread.h
	)
if (NOT CMAKE_LIBRARY_ARCHITECTURE)
	if (CMAKE_SIZEOF_VOID_P EQUAL 8)
		set(CMAKE_LIBRARY_ARCHITECTURE "x64")
		set(NEUROPIX_LINK_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/neuropix-api/lib64/NeuropixAPI_x64_1_17.lib)
	else()
		set(CMAKE_LIBRARY_ARCHITECTURE "x86")
		set(NEUROPIX_LINK_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/neuropix-api/lib32/NeuropixAPI_x86_1_17.lib)
	endif()
endif()

set(NEUROPIX_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/Source/neuropix-api)
target_include_directories(${PLUGIN_NAME} PRIVATE ${NEUROPIX_INCLUDE_DIR})
target_link_libraries(${PLUGIN_NAME} ${NEUROPIX_LINK_DIR})
#optional: create IDE groups
plugin_create_filters()