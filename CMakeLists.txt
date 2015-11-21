cmake_minimum_required(VERSION 2.8.3)
project(rostful_examples)

# Minimal Python module setup
find_package(catkin REQUIRED COMPONENTS roslint rospy)
catkin_python_setup()
catkin_package()

# Lint Python modules
file(GLOB_RECURSE ${PROJECT_NAME}_PY_SCRIPTS
     RELATIVE ${PROJECT_SOURCE_DIR} scripts/*)
roslint_python(${${PROJECT_NAME}_PY_SCRIPTS})

# Install executable scripts
install(DIRECTORY scripts/
        DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
        USE_SOURCE_PERMISSIONS)

install(DIRECTORY interactions/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/interactions
)

install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

