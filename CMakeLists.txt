cmake_minimum_required(VERSION 2.8.3)
project(isam)

set(CMAKE_BUILD_TYPE Release)
LIST( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/CMakeModules )

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

find_package(Eigen3 REQUIRED QUIET)
find_package(Cholmod REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
)

message(${CHOLMOD_INCLUDES})

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${CHOLMOD_INCLUDES}
  ${EIGEN3_INCLUDE_DIR}
)

set(SOURCEFILES
  src/Anchor.cpp
  src/Cholesky.cpp
  src/ChowLiuTree.cpp
  src/covariance.cpp
  src/Covariances.cpp
  src/glc.cpp
  src/GLCReparam.cpp
  src/Node.cpp
  src/numericalDiff.cpp
  src/Optimizer.cpp
  src/OrderedSparseMatrix.cpp
  src/Slam.cpp
  src/SparseMatrix.cpp
  src/SparseSystem.cpp
  src/SparseVector.cpp
  src/util.cpp
)

# isamlib
add_library(isamlib ${SOURCEFILES})
set_property(TARGET isamlib PROPERTY OUTPUT_NAME isam)
target_link_libraries(isamlib ${catkin_LIBRARIES} ${CHOLMOD_LIBRARIES})

