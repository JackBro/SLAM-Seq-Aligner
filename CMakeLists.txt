cmake_minimum_required (VERSION 2.6)
project (Tutorial)

set(CMAKE_VERBOSE_MAKEFILE ON)

# Initialize CXXFLAGS.
#set(CMAKE_CXX_FLAGS "-O0 -std=c++11 -w -g -DDEBUG_log=1")
#set(CMAKE_CXX_FLAGS "-O3 -std=c++11 -w")
set(CMAKE_CXX_FLAGS "-Ofast -std=c++11 -w -DDEBUG_log=3")
#set(CMAKE_CXX_FLAGS "-Ofast -std=c++11 -w")
SET(CMAKE_INCLUDE_PATH ${CMAKE_INCLUDE_PATH} "$HOME/Downloads/boost_1_51_0/")
SET(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} "/opt/local/lib/")

# Compiler-specific C++11 activation.
if ("${CMAKE_CXX_COMPILER_ID}" MATCHES "GNU")
	execute_process(
        COMMAND ${CMAKE_CXX_COMPILER} -dumpversion OUTPUT_VARIABLE GCC_VERSION)
    if (NOT (GCC_VERSION VERSION_GREATER 4.7 OR GCC_VERSION VERSION_EQUAL 4.7))
        message(FATAL_ERROR "${PROJECT_NAME} requires g++ 4.7 or greater.")
    endif ()
elseif ("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
else ()
    message(FATAL_ERROR "Your C++ compiler does not support C++11.")
endif ()


include (${CMAKE_ROOT}/Modules/FindBoost.cmake)

#boost
set(Boost_USE_STATIC_LIBS       OFF)
set(Boost_USE_MULTITHREADED      ON)
set(Boost_USE_STATIC_RUNTIME    OFF)
find_package( Boost COMPONENTS date_time program_options filesystem system serialization system filesystem regex thread iostreams )
find_package( Threads )
find_package( ZLIB )
find_package( CURL )
find_package( OpenSSL )
find_package( PNG )

#htslib
LINK_DIRECTORIES(${CMAKE_BINARY_DIR}/lib)

if(Boost_FOUND AND Threads_FOUND AND ZLIB_FOUND)
	add_executable(bin/FSU_indexer src/indexer.cpp)
	target_link_libraries(bin/FSU_indexer ${CMAKE_SOURCE_DIR}/lib/indexerlib.a ${Boost_LIBRARIES} ${CURL_LIBRARIES} ) 

	add_executable(bin/FSU_searcher src/searcher.cpp)
	target_link_libraries(bin/FSU_searcher ${CMAKE_SOURCE_DIR}/lib/searcherlib.a ${Boost_LIBRARIES} ${CURL_LIBRARIES}) 
endif()
