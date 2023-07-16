cmake_minimum_required(VERSION 3.22)

set(Current-Project-Name Vulkan-Starter)
project(${Current-Project-Name})

# Set C++ standard to a proper standard
set(CMAKE_CXX_STANDARD 23)

# Add the GLFW and Vulkan libraries
find_package(glfw3 REQUIRED)
find_package(Vulkan REQUIRED)
find_package(glm REQUIRED)

# Copy contents of src/shaders to the binary location
add_custom_target(copy_assets
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_LIST_DIR}/src/shaders
        ${CMAKE_CURRENT_BINARY_DIR}/src/shaders
        )

# Dirty way to add all source files in the ./src directory
file(GLOB_RECURSE SRC_FILES "src/*.cpp")

# Create the executable
add_executable(${Current-Project-Name} ${SRC_FILES})

# Link our executable against the libraries
target_link_libraries(${Current-Project-Name} glfw)
target_link_libraries(${Current-Project-Name} Vulkan::Vulkan)
target_link_libraries(${Current-Project-Name} glm::glm)
add_dependencies(${Current-Project-Name} copy_assets)
