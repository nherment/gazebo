add_subdirectory(bandit)
add_subdirectory(blender)
add_subdirectory(epuck)
add_subdirectory(PioneerArm)
add_subdirectory(pioneer2dx)
add_subdirectory(pioneer2at)
add_subdirectory(sonyvid30)
add_subdirectory(rovio)
add_subdirectory(pr2_gripper_meshes)
add_subdirectory(pr2)
add_subdirectory(collada_quad_test)
add_subdirectory(chair3)
add_subdirectory(wg)
add_subdirectory(frypan)
add_subdirectory(people)
add_subdirectory(youbot)
add_subdirectory(hokuyo)
add_subdirectory(quadrotor)
add_subdirectory(willowgarage)
add_subdirectory(kitchen)

set (files hanoi_red_disk.dae
           hanoi_green_disk.dae
           hanoi_blue_disk.dae
           bowl.dae
           test.dae
           human.dae
           coke_can.dae
           cube_20k.stl
           14_4v_cordless_drill.dae
)

install(FILES ${files} DESTINATION ${CMAKE_INSTALL_PREFIX}/share/gazebo-${GAZEBO_VERSION}/Media/models)
