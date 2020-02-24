PROJECT(wingetopt)
cmake_minimum_required(VERSION 2.8)

option(BUILD_SHARED_LIBS "Build the shared library" OFF)

if(BUILD_SHARED_LIBS)
  set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
  add_definitions(-DBUILDING_WINGETOPT_DLL -DWINGETOPT_SHARED_LIB)
endif()

add_library(wingetopt src/getopt.c src/getopt.h)
target_include_directories(wingetopt PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
target_compile_definitions(wingetopt PUBLIC _CRT_SECURE_NO_WARNINGS)

install(FILES src/getopt.h DESTINATION include)

install(TARGETS wingetopt
    RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib)
