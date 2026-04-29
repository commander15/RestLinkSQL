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
else()
    set(QT_MODULES Sql)
endif()

if (RESTLINK_SQL_BUILD_TESTS)
    list(APPEND QT_MODULES Test)
endif()

find_package(Qt6 REQUIRED COMPONENTS ${QT_MODULES})

# RestLink

set(RESTLINK_REQUIRED_VERSION 2.3.1)

if (PROJECT_IS_TOP_LEVEL)
    if (RESTLINK_SQL_BUILD_TESTS)
        set(MODULES COMPONENTS Test)
    endif()

    find_package(RestLink ${RESTLINK_REQUIRED_VERSION} REQUIRED ${MODULES})
elseif (TARGET RestLink)
    if (${RestLink_VERSION} GREATER_EQUAL ${RESTLINK_REQUIRED_VERSION})
        add_library(RestLink::RestLink ALIAS RestLink)
    else()
        message(FATAL_ERROR "RestLink SQL requires at least RestLink ${RESTLINK_REQUIRED_VERSION}")
    endif()
else()
    message(FATAL_ERROR "Can't find RestLink core library")
endif()

add_subdirectory(src)
add_subdirectory(plugin)

if (RESTLINK_SQL_BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
