cmake_minimum_required(VERSION 3.8)
project(more_interfaces)

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rclcpp REQUIRED)

set(msg_files
  "msg/AddressBook.msg"
)
rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
)

ament_export_dependencies(rosidl_default_runtime)

add_executable(publish_address_book
  src/publish_address_book.cpp
)
add_executable(subscribe_address_book
  src/subscribe_address_book.cpp
)


ament_target_dependencies(publish_address_book
  "rclcpp"
)
ament_target_dependencies(subscribe_address_book
  "rclcpp"
)

rosidl_target_interfaces(publish_address_book
  ${PROJECT_NAME} "rosidl_typesupport_cpp"
)
rosidl_target_interfaces(subscribe_address_book
  ${PROJECT_NAME} "rosidl_typesupport_cpp"
)

install(TARGETS 
  publish_address_book
  subscribe_address_book
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()
