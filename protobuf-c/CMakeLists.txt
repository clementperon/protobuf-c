add_library(protobuf-c protobuf-c.c)
set_target_properties(protobuf-c PROPERTIES COMPILE_PDB_NAME protobuf-c)
# Both <protobuf-c/protobuf-c.h> and "protobuf-c.h" are used
target_include_directories(
  protobuf-c PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
                    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
                    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
                    ${PROTOBUF_INCLUDE_DIR})
if(MSVC AND BUILD_SHARED_LIBS)
  target_compile_definitions(protobuf-c PRIVATE -DPROTOBUF_C_EXPORT)
endif()
target_link_libraries(protobuf-c ${protobuf_ABSL_USED_TARGETS}
                      ${protobuf_UTF8_USED_TARGETS})
target_compile_features(protobuf-c PRIVATE cxx_std_17)