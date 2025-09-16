Package Creation 

ros2 pkg create --build-type ament_cmake --license Apache-2.0 <Package-name>

With pluginlib, a constructor without parameters is required

Important note: the polygon_base package in which this node is defined does NOT depend on the polygon_plugins class. The plugins will be loaded dynamically without any dependency needing to be declared.