set(INSTALL_DIR plugins/restlink)
set(OUTPUT_DIR ${CMAKE_BINARY_DIR}/${INSTALL_DIR})

qt_add_plugin(RestLinkSql CLASS_NAME RestLink::Sql::Plugin plugin.cpp)

set_target_properties(
    RestLinkSql
    PROPERTIES
        OUTPUT_NAME restlinksql
        PREFIX      ""
        ARCHIVE_OUTPUT_DIR ${OUTPUT_DIR}
        LIBRARY_OUTPUT_DIR ${OUTPUT_DIR}
        RUNTIME_OUTPUT_DIR ${OUTPUT_DIR}
)

target_link_libraries(
  RestLinkSql
  PRIVATE
    RestLinkSqlLib
)

install(
    TARGETS RestLinkSql
    ARCHIVE DESTINATION ${INSTALL_DIR}
    LIBRARY DESTINATION ${INSTALL_DIR}
    RUNTIME DESTINATION ${INSTALL_DIR}
)
