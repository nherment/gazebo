include (${gazebo_cmake_dir}/GazeboUtils.cmake)

set (sources 
  Animation.cc
  BVHLoader.cc
  ColladaLoader.cc
  Color.cc
  Console.cc
  Diagnostics.cc
  Event.cc
  Events.cc
  Exception.cc
  Image.cc
  KeyFrame.cc
  Material.cc
  Mesh.cc
  MeshLoader.cc
  MeshManager.cc
  PID.cc
  SkeletonAnimation.cc
  Skeleton.cc
  STLLoader.cc
  SystemPaths.cc
  Time.cc
  Timer.cc
)

set (headers 
  Animation.hh
  BVHLoader.hh
  ColladaLoader.hh
  CommonTypes.hh
  Color.hh
  Console.hh
  Diagnostics.hh
  Event.hh
  Events.hh
  Exception.hh
  Image.hh 
  KeyFrame.hh
  Material.hh
  Mesh.hh
  MeshLoader.hh
  MeshManager.hh
  MouseEvent.hh
  PID.hh
  Plugin.hh
  SkeletonAnimation.hh
  Skeleton.hh
  SingletonT.hh
  STLLoader.hh
  SystemPaths.hh
  Time.hh
  Timer.hh
)

set (common_headers "" CACHE INTERNAL "common headers" FORCE)
foreach (hdr ${headers})
  APPEND_TO_CACHED_STRING(common_headers "Common Headers" "#include \"common/${hdr}\"\n")
endforeach()
configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/common.h.in ${CMAKE_CURRENT_BINARY_DIR}/common.h )


gz_add_library(gazebo_common ${sources})
target_link_libraries(gazebo_common gazebo_math
                                    ${libdl_library}
                                    ${tinyxml_libraries}
                                    ${boost_libraries}
                                    ${freeimage_library}
                                    ${tinyxml_libraries})

INSTALL_LIBRARY(gazebo_common)
INSTALL_INCLUDES("common" ${headers} ${CMAKE_CURRENT_BINARY_DIR}/common.h)
