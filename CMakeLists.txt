cmake_minimum_required( VERSION 3.11.0)
# Avoid warning about DOWNLOAD_EXTRACT_TIMESTAMP in CMake 3.24:
if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
    cmake_policy(SET CMP0135 NEW)
endif()

project(ExampleGl)

add_executable(${PROJECT_NAME} ${CMAKE_SOURCE_DIR}/clock.cpp)

set_target_properties(${PROJECT_NAME} PROPERTIES
                      CMAKE_CXX_STANDARD 20
                      CXX_EXTENSIONS OFF
                      )


target_link_libraries(${PROJECT_NAME} PRIVATE GL dcplib)

# ---- ROMDISK generation ----
set(ROMDISK_DIR "romdisk")
kos_add_romdisk(${PROJECT_NAME} ${ROMDISK_DIR})

# ---- CDI Image generation ----
add_custom_target(${PROJECT_NAME}.cdi ALL
                COMMAND ${MKDCDISC} -e ./${PROJECT_NAME}.elf -o ${CMAKE_SOURCE_DIR}/out/${PROJECT_NAME}.cdi -n ${PROJECT_NAME} -v 3
                DEPENDS ${PROJECT_NAME}
                COMMENT "Making CDI image")