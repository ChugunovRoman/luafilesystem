project(xrLuaFS)

set(SRC_FILES
    "src/lfs.h"
    "src/lfs.c"
)

group_sources(SRC_FILES)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
	${LUA_INCLUDE_DIR}
    ${CMAKE_SOURCE_DIR}/Externals
    ${CMAKE_SOURCE_DIR}/Externals/luabind
)

add_library(${PROJECT_NAME} SHARED ${SRC_FILES})

target_link_libraries(${PROJECT_NAME}
    PRIVATE
    xrLuabind
    ${LIBS}
    ${LUA_LIBRARIES}
)

target_compile_definitions(${PROJECT_NAME}
    PRIVATE
    -DLUAMARSHAL_EXPORTS
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    PREFIX ""
)

install(TARGETS ${PROJECT_NAME} LIBRARY
    DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ
)

