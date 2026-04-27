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

add_library(RestLinkTest STATIC main.cpp)
target_compile_definitions(RestLinkTest INTERFACE DATA_DIR="${PROJECT_SOURCE_DIR}/testdata")
target_link_libraries(RestLinkTest PUBLIC GTest::gtest Qt::Core INTERFACE Qt::Test RestLink::RestLink)
link_libraries(RestLinkTest)

# add_subdirectory(core)
add_subdirectory(sql)
