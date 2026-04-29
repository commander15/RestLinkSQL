restlink_add_plugin(
    RestLinkSql
    CLASS_NAME RestLink::Sql::Plugin
    SOURCES plugin.cpp
    LINK_LIBRARIES RestLinkSqlLib
)

restlink_install_plugin(RestLinkSql)
