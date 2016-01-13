include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
)

set(
    Myappbackend_SRCS
    modules/Myapp/backend.cpp
    modules/Myapp/mytype.cpp
)

add_library(Myappbackend MODULE
    ${Myappbackend_SRCS}
)

set_target_properties(Myappbackend PROPERTIES
         LIBRARY_OUTPUT_DIRECTORY Myapp)

qt5_use_modules(Myappbackend Gui Qml Quick)

# Copy qmldir file to build dir for running in QtCreator
add_custom_target(Myappbackend-qmldir ALL
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/modules/Myapp/qmldir ${CMAKE_CURRENT_BINARY_DIR}/Myapp
    DEPENDS ${QMLFILES}
)

# Install plugin file
install(TARGETS Myappbackend DESTINATION ${QT_IMPORTS_DIR}/Myapp/)
install(FILES   modules/Myapp/qmldir DESTINATION ${QT_IMPORTS_DIR}/Myapp/)

