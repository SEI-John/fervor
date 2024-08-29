cmake_minimum_required(VERSION 3.16)
project(Sample VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)

find_package(QT NAMES Qt5 Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui)

qt_standard_project_setup()

qt_add_executable(Sample WIN32 MACOSX_BUNDLE
    main.cpp
    mainwindow.cpp mainwindow.h mainwindow.ui
)
target_link_libraries(Sample PRIVATE
    Qt::Core
    Qt::Gui
)

install(TARGETS Sample
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET Sample
    FILENAME_VARIABLE deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
