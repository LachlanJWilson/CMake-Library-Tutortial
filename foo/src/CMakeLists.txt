set(FILES "")
set(SUBDIRECTORIES "Foo")
set(RELATIVE_PATH "src")

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