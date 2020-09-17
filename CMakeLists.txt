cmake_minimum_required(VERSION "3.18.2")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib") #sets output dir for archive targets
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BONARY_DIR}/lib") #sets output dir for library targets
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin") #sets output dir for runtime targets

set(VALID_BUILD_TYPES "Release" "Debug" "MinSizeRel" "RelWithDebInfo")

option(BUILD_SHARED_LIBS "True when building a shared library" TRUE) #adds the BUILD_SHARED_LIBS variable to the cmake cache with a value of true.

project("Foo")

#set CMAKE_BUILD_TYPE default value
if(NOT CMAKE_CONFIGURATION_TYPES) #if not using multi configuration generator
	if("${CMAKE_BUILD_TYPE}" STREQUAL "") #is CMAKE_BUILD_TYPE is an empty string
		set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build configuration" FORCE) #set string to Release
	endif()
endif()

#validate CMAKE_BUILD_TYPE
#Single configuration generators do not use CMAKE_CONFIGURATION_TYPES, therefore the below does nothing for multi configuration generators
if(NOT CMAKE_CONFIGURATION_TYPES)
	list(FIND VALID_BUILD_TYPES "${CMAKE_BUILD_TYPE}" INDEX)
	if(${INDEX} MATCHES -1)
		message(FATAL_ERROR "Invalid build type. Valid types are [${VALID_BUILD_TYPES}]")
	endif()
endif()

add_subdirectory("foo")
add_subdirectory("examples")