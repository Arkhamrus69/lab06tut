cmake_minimum_required(VERSION 3.10)

project(lab06 VERSION 0.1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(solver)

install(TARGETS solver
    RUNTIME DESTINATION bin
)

include(CPackConfig.cmake)
