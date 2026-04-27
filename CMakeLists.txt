cmake_minimum_required(VERSION 3.30)

project(RestLinkSQL
    VERSION 1.0.0
)

option(RESTLINK_SQL_BUILD_TESTS "Build plugin tests" OFF)

# Qt

if (PROJECT_IS_TOP_LEVEL)
    set(CMAKE_AUTOMOC ON)
    set(CMAKE_AUTORCC ON)

    set(QT_MODULES Core Network Sql)
    if (RESTLINK_SQL_BUILD_TESTS)
        list(APPEND QT_MODULES Test)
    endif()
else()
    set(QT_MODULES Sql)
endif()

find_package(Qt6 REQUIRED COMPONENTS ${QT_MODULES})

# RestLink

option(RESTLINK_BUILD_CLI   OFF)
option(RESTLINK_BUILD_QML   OFF)
option(RESTLINK_BUILD_SQL   OFF)
option(RESTLINK_BUILD_EXCEL OFF)

if (TARGET RestLink)
    add_library(RestLink::RestLink ALIAS RestLink)
else()
    find_package(RestLink 2.3.0 REQUIRED)
endif()

add_subdirectory(src)
add_subdirectory(plugin)

if (RESTLINK_SQL_BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
