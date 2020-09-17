add_library("${PROJECT_NAME}" "")
add_library(Foo::Foo ALIAS "${PROJECT_NAME}") #allows us to refer to the foo library as Foo::Foo

target_include_directories("${PROJECT_NAME}" PUBLIC
	"$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
	"$<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>" #foo_export.h
	#The above generator expression adds ${CMAKE_CURRENT_BINARY_DIR} to our list of include directories for the build directory
	#as we install the foo_export.h file in the include directory we only have to use the install generator once
	"$<INSTALL_INTERFACE:include>" #${CMAKE_INSTALL_PREFIX}/include
)

#PRIVATE is a Build Requirement
#INTERFACE is a Usage Requirement
#PUBLIC is both a Build and Usage Requirement

#Build Requirements is anything that is required to build a target
#Usage Requirements is anything that is required to link against our target

#both of the above directories are required for both building and linking against our target, hence they are PUBLIC

if(NOT BUILD_SHARED_LIBS) #if false library is static
	set(STATIC_POSTFIX "-s") #therefore set postfix
	set_target_properties("${PROJECT_NAME}" PROPERTIES
	COMPILE_FLAGS -DFOO_STATIC_DEFINE)
endif()

#Rename target Foo 
set_target_properties("${PROJECT_NAME}" PROPERTIES
	DEBUG_POSTFIX "${STATIC_POSTFIX}-d" #will be added to the end of the library name whenever it is built in debug mode
	RELEASE_POSTFIX "${STATIC_POSTFIX}" #will be added to the end of the library name whenever it is built in release mode
	MINSIZEREL_POSTFIX "${STATIC_POSTFIX}-mr" #minimum size release postfix
	RELWITHDEBINFO_POSTFIX "${STATIC_POSTFIX}-rd" #release with debug info postfix
)

include("GenerateExportHeader") #including this gives us the option to use the generate_export_header 
generate_export_header("${PROJECT_NAME}") #generates a header file thats called PROJECT_NAME_export.h
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/foo_export.h" DESTINATION "include") #install header in the include directories
#as this process uses the CMAKE_CURRENT_BINARY_DIR dir, we need to add this above in the target_include_directories


#letting the program know about the include and src subdirectories. 
add_subdirectory("include")
add_subdirectory("src")