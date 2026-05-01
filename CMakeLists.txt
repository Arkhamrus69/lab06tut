cmake_minimum_required(VERSION 3.10)

project(lab06 VERSION 0.1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_TESTS "Build tests" OFF)
option(COLLECT_COVERAGE "Collect coverage" OFF)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(solver)

if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/banking/CMakeLists.txt")
    add_subdirectory(banking)
endif()

if(BUILD_TESTS)
    enable_testing()

    add_subdirectory(third-party/gtest)

    file(GLOB TEST_SOURCES
        "${CMAKE_CURRENT_SOURCE_DIR}/tests/*.cpp"
    )

    add_executable(check
        ${TEST_SOURCES}
    )

    if(TARGET transaction AND TARGET account)
        target_link_libraries(check
            transaction
            account
            gmock_main
        )
    else()
        target_link_libraries(check
            gtest_main
            gmock_main
        )
    endif()

    add_test(NAME check COMMAND check)
endif()

install(TARGETS solver
    RUNTIME DESTINATION bin
)

include(CPackConfig.cmake)
