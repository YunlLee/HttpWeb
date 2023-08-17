cmake_minimum_required(VERSION 3.20)

project(main)

set(CMAKE_CXX_STANDARD 17)

set(MYSQL_ROOT_LIB /usr/lib)
message("Value of my_variable: ${MYSQL_ROOT_LIB}")
include_directories(
    ${CMAKE_SOURCE_DIR}/sql
    ${CMAKE_SOURCE_DIR}/log
    ${CMAKE_SOURCE_DIR}/lock
    ${CMAKE_SOURCE_DIR}/threadpool
    ${CMAKE_SOURCE_DIR}/timer
    ${CMAKE_SOURCE_DIR}/http
)

file(GLOB_RECURSE headers CONFIGURE_DEPENDS sql/*.h log/*.h lock/*.h threadpool/*.h timer/*.h http/*.h)
file(GLOB_RECURSE sourses CONFIGURE_DEPENDS sql/*.cpp log/*.cpp lock/*.cpp timer/*.cpp http/*.cpp)
add_executable(main main.cpp config.cpp config.h webserver.cpp webserver.h ${sourses} ${headers} )
target_link_directories(main PUBLIC ${MYSQL_ROOT_LIB})
target_link_libraries(main mysqlclient)