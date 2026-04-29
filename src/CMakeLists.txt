qt_add_library(
  RestLinkSqlLib STATIC
  global.h
  debug.h debug.cpp
  api.h api.cpp
)

set(UTILS_SOURCES
  utils/jsonutils.h utils/jsonutils.cpp
  utils/sqlutils.h utils/sqlutils.cpp
  utils/databaseutils.h utils/databaseutils.cpp
  utils/querybuilder.h utils/querybuilder.cpp
  utils/queryrunner.h utils/queryrunner.cpp
)

set(META_SOURCES
  meta/parseddata.h meta/parseddata.cpp
  meta/endpointinfo.h meta/endpointinfo.cpp
  meta/sqlqueryinfo.h meta/sqlqueryinfo.cpp
  meta/resourceinfo.h meta/resourceinfo.cpp
  meta/relationinfo.h meta/relationinfo.cpp
)

set(ROUTING_SOURCES
  routing/router.h routing/router.cpp
  routing/modelcontroller.h routing/modelcontroller.cpp
)

set(DATA_SOURCES
  data/crudinterface.h data/crudinterface.cpp
  data/model.h data/model.cpp
  data/relation.h data/relation.cpp
)

set(RELATIONS_SOURCES
  relations/relation_api_impl.h relations/relation_api_impl.cpp
  relations/relation_base_impl.h relations/relation_base_impl.cpp
)

target_sources(
  RestLinkSqlLib
  PRIVATE
    ${DATA_SOURCES}
    ${RELATIONS_SOURCES}
    ${ROUTING_SOURCES}
    ${META_SOURCES}
    ${UTILS_SOURCES}
)

target_include_directories(RestLinkSqlLib
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)

target_link_libraries(
  RestLinkSqlLib
  PUBLIC
    RestLink::RestLink
    Qt::Sql
)

target_compile_definitions(
  RestLinkSqlLib
  PUBLIC
    RESTLINK_SQL_VERSION_STR="${PROJECT_VERSION}"
)
