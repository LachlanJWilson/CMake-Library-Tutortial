add_executable("Example" "Main.cpp") #creates executable with source file of Main.cpp
target_link_libraries("Example" PRIVATE Foo::Foo) #links to Foo library
#Remember PRIVATE is for BUILD, INTERFACE is for usage and PUBLIC is both. 