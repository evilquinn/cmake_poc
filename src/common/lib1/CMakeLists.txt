
add_library ( lib1 STATIC lib1.cpp )

target_include_directories(lib1 PUBLIC
    $<INSTALL_INTERFACE:include>)


install(TARGETS lib1
        EXPORT cmake_poc_export
        DESTINATION ${CMAKE_BINARY_DIR}/lib)


