cmake_minimum_required(VERSION 2.8.11)
project(qtorm)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

# Find the QtWidgets library
#find_package(Qt5Core)
find_package(Qt5 REQUIRED COMPONENTS Core  Sql)

include(GNUInstallDirs)

add_definitions(-fPIC)
set(CMAKE_CXX_STANDARD 11)

include_directories(
        ${CMAKE_CURRENT_BINARY_DIR}
        ${Qt5Core_INCLUDE_DIRS}
        ${Qt5Sql_INCLUDE_DIRS}
        ${Qt5_INCLUDE_DIRS}
        ${QT_QT_INCLUDE_DIR}
)

# Sources
set(qtorm_SRCS
    qassign.cpp
    qdatetimefield.cpp
    qdoublefield.cpp
    qf.cpp
    qfield.cpp
    qforeignkey.cpp
    qintfield.cpp
    qmodel.cpp
    qqueryset.cpp
    qstringfield.cpp
    qwhere.cpp
    qtormdatabase.cpp
)

set(qtorm_HEADERS
    qassign.h
    qdatetimefield.h
    qdoublefield.h
    qf.h
    qfield.h
    qfield_p.h
    qforeignkey.h
    qforeignkey_p.h
    qintfield.h
    qmodel.h
    qqueryset.h
    qstringfield.h
    qwhere.h
    qtormdatabase.h
)

# Automoc
#qt5_automoc(${qtorm_SRCS})

# Shared library
add_library(qtorm SHARED ${qtorm_SRCS})

set_target_properties(qtorm PROPERTIES
    VERSION 0.1.0
    SOVERSION 0.1.0
)
target_link_libraries(qtorm
    ${QT_QTCORE_LIBRARY}
    ${QT_QTSQL_LIBRARY}
)

install(TARGETS qtorm LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
install(FILES ${qtorm_HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qtorm)
