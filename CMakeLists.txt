cmake_minimum_required(VERSION 3.22)

project(libltc)

option(BUILD_EXAMPLES "Build examples" OFF)

file(GLOB_RECURSE sources src/*.c src/*.h)

add_library(libltc STATIC ${sources})
target_include_directories(libltc PUBLIC src)

if(${BUILD_EXAMPLES})
    file(GLOB_RECURSE tests tests/*.c tests/*.h)

	add_executable(libltc_decode tests/ltcdecode.c)
	add_executable(libltc_encode tests/ltcencode.c)
	add_executable(libltc_encode_example tests/example_encode.c)

	target_link_libraries(libltc_decode libltc)
	target_link_libraries(libltc_encode libltc)
	target_link_libraries(libltc_encode_example libltc)

	target_include_directories(libltc_decode PUBLIC src)
	target_include_directories(libltc_encode PUBLIC src)
	target_include_directories(libltc_encode_example PUBLIC src)
endif(${BUILD_EXAMPLES})

