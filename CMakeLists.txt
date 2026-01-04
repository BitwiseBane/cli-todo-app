cmake_minimum_required(VERSION 3.25)

project(todo-app VERSION 1.0.0 LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Include directories
include_directories(${PROJECT_SOURCE_DIR}/include)

# Source files
set(SOURCES
    src/main.cpp
    src/Task.cpp
    src/TaskManager.cpp
    src/FileHandler.cpp
    src/UIManager.cpp
    src/Utils.cpp
)

# Create executable
add_executable(todo-app ${SOURCES})

# Platform-specific settings
if(WIN32)
    # Windows-specific settings
    target_compile_definitions(todo-app PRIVATE _WIN32)
elseif(APPLE)
    # macOS-specific settings
    target_compile_definitions(todo-app PRIVATE __APPLE__)
elseif(UNIX)
    # Linux-specific settings
    target_compile_definitions(todo-app PRIVATE __linux__)
endif()

# Compiler warnings
if(MSVC)
    target_compile_options(todo-app PRIVATE /W4)
else()
    target_compile_options(todo-app PRIVATE -Wall -Wextra -Wpedantic)
endif()

# Installation rules (optional)
install(TARGETS todo-app DESTINATION bin)