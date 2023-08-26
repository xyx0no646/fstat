
cmake_minimum_required(VERSION 3.12)
project(fstat_krkrsdl2)

include(FetchContent)

FetchContent_Declare(
	krkrsdl2-ncbind
	GIT_REPOSITORY https://github.com/krkrsdl2/ncbind.git
	GIT_TAG origin/krkrsdl2
)

FetchContent_MakeAvailable(krkrsdl2-ncbind)

set(FSTAT_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(STRINGS ${FSTAT_SRC_DIR}/src_list/sources.txt FSTAT_SRC)
file(STRINGS ${FSTAT_SRC_DIR}/src_list/includes.txt FSTAT_INCLUDES)
list(TRANSFORM FSTAT_SRC PREPEND ${FSTAT_SRC_DIR}/)
list(TRANSFORM FSTAT_INCLUDES PREPEND ${FSTAT_SRC_DIR}/)

add_library(fstat MODULE)
set_target_properties(fstat PROPERTIES CXX_STANDARD 11)
set_target_properties(fstat PROPERTIES PREFIX "")
target_sources(fstat PRIVATE ${FSTAT_SRC})
target_include_directories(fstat PRIVATE ${FSTAT_INCLUDES})
target_link_libraries(fstat ncbind)
