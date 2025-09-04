cmake_minimum_required(VERSION 3.8)
project(tutorial_interfaces)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rclcpp REQUIRED)

set(msg_files
  "msg/AddressBook.msg"
  "msg/Num.msg"
  "msg/Sphere.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  # "msg/Num.msg"
  # "msg/Sphere.msg"
  ${msg_files}
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)

rosidl_get_typesupport_target(cpp_typesupport_target
  ${PROJECT_NAME} rosidl_typesupport_cpp)                                 # To use the generated message types in C++ from the same package


add_executable(publish_address_book src/publish_address_book.cpp)
ament_target_dependencies(publish_address_book rclcpp)
target_link_libraries(publish_address_book "${cpp_typesupport_target}")   # To use the generated message types in C++ from the same package

install(TARGETS
    publish_address_book
  DESTINATION lib/${PROJECT_NAME})

ament_package()
