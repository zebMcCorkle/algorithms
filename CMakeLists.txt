cmake_minimum_required(VERSION 3.2)
project(algorithms)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Werror -pedantic")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall -Werror -pedantic")

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -O3")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS} -O3")

set(HEADERS tree_map.h hash_map.h map.h stack.h)
set(SOURCE_FILES tree_map.c hash_map.c ${HEADERS} stack.c)
set(TEST_FILES test/tree_map.c test/test.c test/hash_map.c test/hash_map.h test/config.h test/stack.c test/stack.h)
add_executable(test_algorithms ${SOURCE_FILES} ${TEST_FILES})
add_library(algorithms ${SOURCE_FILES})
add_library(shared_algorithms SHARED ${SOURCE_FILES})

if (NOT WIN32)
    set_target_properties(shared_algorithms PROPERTIES OUTPUT_NAME algorithms)
endif()

install(TARGETS algorithms shared_algorithms
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib)
install(FILES ${HEADERS}
        DESTINATION include/zebMcCorkle/algorithms)