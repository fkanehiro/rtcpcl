set(rtc_name rtcpclrainbowtube)

# Install component header files
set(comp_headers ${rtc_name}.h)
install(FILES ${comp_headers} DESTINATION ${INCLUDE_INSTALL_DIR}
    COMPONENT ${rtc_name})

# Component target
set(comp_srcs ${rtc_name}.cpp)
include_directories(${IDL_HEADERS_DIR} ${DEPS_INCLUDE_DIRS})
add_library(${rtc_name} SHARED ${comp_srcs} ${IDL_TYPE_SOURCES})
target_link_libraries(${rtc_name} rtcpcl_pointcloud_type ${DEPS_LIBRARIES} rt)
install(TARGETS ${rtc_name} LIBRARY DESTINATION ${LIB_INSTALL_DIR}
    COMPONENT ${rtc_name})

MAKE_STANDALONE(${PROJECT_SOURCE_DIR}/cmake/standalone.cpp.in
    RTCPCLRainbowTube ${rtc_name}
    ${CMAKE_CURRENT_SOURCE_DIR}/${rtc_name}.h)

