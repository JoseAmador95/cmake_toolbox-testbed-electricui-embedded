set(CMOCK_PLUGINS ignore ignore_arg expect expect_any_args callback)
set(CMOCK_ENFORCE_STRICT_ORDERING ON)
set(CMOCK_MEM_DYNAMIC ON)

include(Ceedling)

set(EUI_TEST_ROOT "${CMAKE_CURRENT_LIST_DIR}/test")
file(GLOB_RECURSE EUI_UNIT_TEST_SOURCES CONFIGURE_DEPENDS "${EUI_TEST_ROOT}/test_*.c")

if(NOT EUI_UNIT_TEST_SOURCES)
    message(WARNING "No unit tests found in ${EUI_TEST_ROOT}")
endif()

list(SORT EUI_UNIT_TEST_SOURCES)

foreach(test_source IN LISTS EUI_UNIT_TEST_SOURCES)
    cmake_path(GET test_source STEM test_name)
    set(test_target "eui_${test_name}")

    Ceedling_AddUnitTest(
        NAME ${test_target}
        UNIT_TEST ${test_source}
        TARGET electricui
    )
endforeach()
