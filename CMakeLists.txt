cmake_minimum_required( VERSION 3.11.0)
# Avoid warning about DOWNLOAD_EXTRACT_TIMESTAMP in CMake 3.24:
if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
    cmake_policy(SET CMP0135 NEW)
endif()

project(dc-cmake-examples CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
include(NoInSourceBuilds)
# ------------------------------------------ #
# Global cmake variables
# ------------------------------------------ #
set(CMAKE_CXX_STANDARD 20)

# ------------------------------------------ #
# Subdirectories
# ------------------------------------------ #
add_subdirectory(src)