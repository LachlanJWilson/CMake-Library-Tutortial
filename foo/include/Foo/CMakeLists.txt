set(FILES "${CMAKE_CURRENT_SOURCE_DIR}/Hello.h")
set(SUBDIRECTORIES "")
set(RELATIVE_PATH "include/Foo")

#Add all subdirectories 
foreach(VAR ${SUBDIRECTORIES}) #for each subdirectory specified
	add_subdirectory(${VAR}) #add the subdirectory
endforeach()

if(FILES)
	#Add dource files to target
	target_sources("${PROJECT_NAME}" PRIVATE ${FILES})
	
	#Install our source files
	install(FILES ${FILES} DESTINATION ${RELATIVE_PATH})
endif()