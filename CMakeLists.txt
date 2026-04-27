cmake_minimum_required(VERSION 3.30)

project(RestLinkSQL
    VERSION 1.0.0
)

# Qt

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt6 REQUIRED COMPONENTS Core Sql)

# RestLink

option(RESTLINK_BUILD_CLI   OFF)
option(RESTLINK_BUILD_QML   OFF)
option(RESTLINK_BUILD_SQL   OFF)
option(RESTLINK_BUILD_EXCEL OFF)

include(FetchContent)

FetchContent_Declare(
    RestLink
    GIT_REPOSITORY "https://github.com/commander15/RestLink.git"
    GIT_TAG "6a9f0b5729f03845ff7ccd3f2ec056cf202323d2"
)

FetchContent_MakeAvailable(RestLink)

add_subdirectory(src)
