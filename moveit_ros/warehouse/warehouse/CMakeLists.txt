set(MOVEIT_LIB_NAME moveit_warehouse)

add_library(${MOVEIT_LIB_NAME}
  src/moveit_message_storage.cpp
  src/planning_scene_storage.cpp
  src/planning_scene_world_storage.cpp
  src/constraints_storage.cpp
  src/trajectory_constraints_storage.cpp
  src/state_storage.cpp
  src/warehouse_connector.cpp)
set_target_properties(${MOVEIT_LIB_NAME} PROPERTIES VERSION "${${PROJECT_NAME}_VERSION}")
target_link_libraries(${MOVEIT_LIB_NAME} ${rclcpp_LIBRARIES} ${Boost_LIBRARIES})

add_executable(moveit_warehouse_broadcast src/broadcast.cpp)
ament_target_dependencies(moveit_warehouse_broadcast ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES} )

add_executable(moveit_save_to_warehouse src/save_to_warehouse.cpp)
ament_target_dependencies(moveit_save_to_warehouse ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES})

add_executable(moveit_warehouse_import_from_text src/import_from_text.cpp)
ament_target_dependencies(moveit_warehouse_import_from_text ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES})

add_executable(moveit_warehouse_save_as_text src/save_as_text.cpp)
ament_target_dependencies(moveit_warehouse_save_as_text ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES})

add_executable(moveit_init_demo_warehouse src/initialize_demo_db.cpp)
ament_target_dependencies(moveit_init_demo_warehouse ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES})

add_executable(moveit_warehouse_services src/warehouse_services.cpp)
ament_target_dependencies(moveit_warehouse_services ${rclcpp_LIBRARIES} ${MOVEIT_LIB_NAME} ${Boost_LIBRARIES})

install(
  TARGETS
    ${MOVEIT_LIB_NAME}
    moveit_save_to_warehouse
    moveit_warehouse_broadcast
    moveit_warehouse_import_from_text
    moveit_warehouse_save_as_text
    moveit_init_demo_warehouse
    moveit_warehouse_services
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib/${PROJECT_NAME})

install(DIRECTORY include/ DESTINATION include)
