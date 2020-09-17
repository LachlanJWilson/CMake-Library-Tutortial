cmake_minimum_required(VERSION "3.18.2")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib") #sets output dir for archive targets
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BONARY_DIR}/lib") #sets output dir for library targets
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin") #sets output dir for runtime targets

option(BUILD_SHARED_LIBS "True when building a shared library" TRUE) #adds the BUILD_SHARED_LIBS variable to the cmake cache with a value of true.

project("Foo")

add_subdirectory("foo")

add_subdirectory("examples")