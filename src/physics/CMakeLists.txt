include (${gazebo_cmake_dir}/GazeboUtils.cmake)
add_subdirectory(ode)

if (HAVE_BULLET)
  add_subdirectory(bullet)
endif()

set (sources
  Actor.cc
  Base.cc
  BoxShape.cc
  Collision.cc
  CollisionState.cc
  Contact.cc
  CylinderShape.cc
  Entity.cc
  Gripper.cc
  HeightmapShape.cc
  Inertial.cc
  Joint.cc
  JointController.cc
  JointState.cc
  Link.cc
  LinkState.cc
  MapShape.cc
  Model.cc
  ModelState.cc
  MultiRayShape.cc
  Physics.cc
  PhysicsEngine.cc
  PhysicsFactory.cc
  PlaneShape.cc
  RayShape.cc
  Shape.cc
  SphereShape.cc
  State.cc
  SurfaceParams.cc
  TrimeshShape.cc
  World.cc
  WorldState.cc
) 

set (headers
  Actor.hh
  BallJoint.hh
  Base.hh
  BoxShape.hh
  Collision.hh
  CollisionState.hh
  Contact.hh
  CylinderShape.hh
  Entity.hh
  HeightmapShape.hh
  Hinge2Joint.hh
  HingeJoint.hh
  Inertial.hh
  Gripper.hh
  Joint.hh
  JointController.hh
  JointFeedback.hh
  JointState.hh
  Link.hh
  LinkState.hh
  MapShape.hh
  Model.hh
  ModelState.hh
  MultiRayShape.hh
  Physics.hh
  PhysicsEngine.hh
  PhysicsFactory.hh
  PhysicsTypes.hh
  PlaneShape.hh
  RayShape.hh
  Shape.hh
  ScrewJoint.hh
  SliderJoint.hh
  SphereShape.hh
  State.hh
  SurfaceParams.hh
  TrimeshShape.hh
  UniversalJoint.hh
  World.hh
  WorldState.hh)

set (physics_headers "" CACHE INTERNAL "physics headers" FORCE)
foreach (hdr ${headers})
  APPEND_TO_CACHED_STRING(physics_headers "Physics Headers" "#include \"physics/${hdr}\"\n")
endforeach()
configure_file (${CMAKE_CURRENT_SOURCE_DIR}/physics.h.in ${CMAKE_CURRENT_BINARY_DIR}/physics.h)

gz_add_library(gazebo_physics ${sources})

target_link_libraries(gazebo_physics
  gazebo_common 
  gazebo_sdf_interface
  gazebo_physics_ode
  ${TBB_LIBRARIES} 
  ${libtool_library} 
  ${boost_libraries}
  ${tinyxml_libraries})

if (HAVE_BULLET)
  target_link_libraries(gazebo_physics gazebo_physics_bullet)
endif()

gz_add_executable(gzphysics server.cc)
target_link_libraries(gzphysics gazebo_common
                                gazebo_transport
                                gazebo_physics
                                gazebo_sensors
                                gazebo_sdf_interface
                                gazebo_msgs
                                pthread
                                )

INSTALL_EXECUTABLE( gzphysics )
INSTALL_LIBRARY(gazebo_physics)
INSTALL_INCLUDES("physics" ${headers} ${CMAKE_CURRENT_BINARY_DIR}/physics.h)
