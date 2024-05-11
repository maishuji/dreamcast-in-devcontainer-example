cmake_minimum_required( VERSION 3.11.0)
# Avoid warning about DOWNLOAD_EXTRACT_TIMESTAMP in CMake 3.24:
if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
    cmake_policy(SET CMP0135 NEW)
endif()
set(TARGET_NAME "clock-example")
add_executable(${TARGET_NAME} ${CMAKE_CURRENT_SOURCE_DIR}/clock.cpp)

set_target_properties(${TARGET_NAME} PROPERTIES
                      CMAKE_CXX_STANDARD 20
                      CXX_EXTENSIONS OFF
                      )

target_link_libraries(${TARGET_NAME} PRIVATE GL dcplib)

# ---- ROMDISK generation ----
set(ROMDISK_DIR "romdisk")
kos_add_romdisk(${TARGET_NAME} ${ROMDISK_DIR})

# ---- CDI Image generation ----
add_custom_target(${TARGET_NAME}.cdi ALL
                COMMAND ${MKDCDISC} -e ./${TARGET_NAME}.elf -o ${PROJECT_SOURCE_DIR}/out/${TARGET_NAME}.cdi -n ${TARGET_NAME} -v 3
                DEPENDS ${TARGET_NAME}
                COMMENT "Making CDI image")