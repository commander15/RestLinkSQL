include(FetchContent)

FetchContent_Declare(
    GTest
    GIT_REPOSITORY "https://github.com/google/googletest.git"
    GIT_TAG "v1.14.0"
    FIND_PACKAGE_ARGS NAMES GTest 1.14.0
)

FetchContent_MakeAvailable(GTest)
if (NOT TARGET GTest::gtest)
    add_library(GTest::gtest ALIAS gtest)
endif()

add_library(RestLinkCoreTest STATIC main.cpp)
target_compile_definitions(RestLinkCoreTest INTERFACE DATA_DIR="${PROJECT_SOURCE_DIR}/testdata")
target_link_libraries(RestLinkCoreTest PUBLIC GTest::gtest Qt::Core INTERFACE Qt::Test RestLink::RestLink)
link_libraries(RestLinkCoreTest)

# add_subdirectory(core)
add_subdirectory(sql)
