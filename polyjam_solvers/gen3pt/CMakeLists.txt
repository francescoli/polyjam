cmake_minimum_required(VERSION 2.4.6)
project(test_gen3pt)

# Set the build type.  Options are:
#
#  None (CMAKE_C_FLAGS or CMAKE_CXX_FLAGS used)
#  Debug (CMAKE_C_FLAGS_DEBUG or CMAKE_CXX_FLAGS_DEBUG)
#  Release (CMAKE_C_FLAGS_RELEASE or CMAKE_CXX_FLAGS_RELEASE)
#  RelWithDebInfo (CMAKE_C_FLAGS_RELWITHDEBINFO or CMAKE_CXX_FLAGS_RELWITHDEBINFO
#  MinSizeRel (CMAKE_C_FLAGS_MINSIZEREL or CMAKE_CXX_FLAGS_MINSIZEREL) 

set(CMAKE_BUILD_TYPE Release)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

add_definitions (-Wall -march=native -O3)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/modules/")
find_package(Eigen REQUIRED)
find_package(boost REQUIRED)

include_directories(${EIGEN_INCLUDE_DIRS} ${EIGEN_INCLUDE_DIR}/unsupported ${Boost_INCLUDE_DIRS} ${PROJECT_SOURCE_DIR}/include)

add_library( random_generators SHARED random_generators.cpp random_generators.hpp experiment_helpers.cpp experiment_helpers.hpp time_measurement.cpp time_measurement.hpp )

add_executable( test_gen3pt test.cpp gen3pt.cpp GaussJordan.cpp )
target_link_libraries( test_gen3pt random_generators )
