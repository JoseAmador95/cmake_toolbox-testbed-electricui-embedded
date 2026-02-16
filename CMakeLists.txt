cmake_minimum_required(VERSION 3.22)

set(PROJECT_VERSION 0.0.8)

project(electricui-embedded VERSION ${PROJECT_VERSION})

add_library(
    electricui
    STATIC
    src/electricui.c
    src/eui_utilities.c
    src/transports/eui_binary_transport.c
)

target_include_directories(
    electricui
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/src
        ${CMAKE_CURRENT_SOURCE_DIR}/src/transports
)

option(EUI_ENABLE_TESTS "Build unit tests with CMake Toolbox" ${PROJECT_IS_TOP_LEVEL})

if(EUI_ENABLE_TESTS)
    include(FetchContent)
    FetchContent_Declare(
        cmake_toolbox
        GIT_REPOSITORY "https://github.com/JoseAmador95/cmake_toolbox.git"
        GIT_TAG main
    )
    FetchContent_MakeAvailable(cmake_toolbox)

    list(APPEND CMAKE_MODULE_PATH "${cmake_toolbox_SOURCE_DIR}/cmake")

    enable_testing()
    add_subdirectory(test)
endif()
