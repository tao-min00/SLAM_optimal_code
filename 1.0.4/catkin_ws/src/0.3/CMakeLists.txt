cmake_minimum_required( VERSION 2.8 )
project ( myslam )

set( CMAKE_CXX_COMPILER "g++" )
set( CMAKE_BUILD_TYPE "Release" )
#set( CMAKE_CXX_FLAGS "-std=c++14 -march=native -O3" )
set( CMAKE_CXX_FLAGS "-std=c++14 -O3" )


#set( CMAKE_CXX_FLAGS "-std=c++11 -O3" )
#set( CMAKE_CXX_FLAGS "-std=c++14 -march=native -O3" )
#set(CMAKE_CXX_FLAGS "-std=c++14 -O2 ${SSE_FLAGS} -msse4")
#set(CMAKE_CXX_FLAGS "-std=c++14 -O2 ${SSE_FLAGS} -g ${CMAKE_CXX_FLAGS} -mpopcnt")
#set(CMAKE_CXX_STANDARD 11) 
#set(CMAKE_CXX_STANDARD 14)



list( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules )
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin )
set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib )

############### dependencies ######################

# Eigen
include_directories( "/usr/include/eigen3" )
# OpenCV
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )
# Sophus 
find_package( Sophus REQUIRED )
include_directories( ${Sophus_INCLUDE_DIRS} )

find_package(FMT REQUIRED)
set(FMT_LIBRARIES fmt: :fmt)


# G2O
find_package( G2O REQUIRED )
include_directories( ${G2O_INCLUDE_DIRS} )

set( THIRD_PARTY_LIBS 
    ${OpenCV_LIBS}
    ${Sophus_LIBRARIES}
    fmt::fmt
    g2o_core g2o_stuff g2o_types_sba
)
############### dependencies ######################
include_directories( ${PROJECT_SOURCE_DIR}/include )
add_subdirectory( src )
add_subdirectory( test )
