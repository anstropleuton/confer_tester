cmake_minimum_required(VERSION 3.30)

project(confer_tester
    VERSION 1.0.0.0
    DESCRIPTION "Confer Tester is a testing framework for Anstro Pleuton's libraries and programs."
    LANGUAGES CXX
)

option(CONFER_TESTER_BUILD_TESTS "Build Confer Tester tests" OFF)
option(CONFER_TESTER_BUILD_EXAMPLES "Build Confer Tester examples" OFF)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

set(DOXYGEN_CONFER_TESTER_PROJECT_VERSION ${PROJECT_VERSION})
set(DOXYGEN_CONFER_TESTER_OUTPUT_DIR "${CMAKE_CURRENT_BINARY_DIR}/docs")

configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/include/confer_tester_config.hpp.in"
    "${CMAKE_CURRENT_BINARY_DIR}/confer_tester_config.hpp"
)
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/confer_tester.pc.in"
    "${CMAKE_CURRENT_BINARY_DIR}/confer_tester.pc"
)
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in"
    "${CMAKE_CURRENT_BINARY_DIR}/Doxyfile"
    @ONLY
)

set(CONFER_TESTER_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/confer_tester.cpp"
)
set(CONFER_TESTER_HEADERS
    "${CMAKE_CURRENT_BINARY_DIR}/confer_tester_config.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/include/confer_tester.hpp"
)
set(CONFER_TESTER_INCLUDE_DIRS
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
    "${CMAKE_CURRENT_BINARY_DIR}"
)

add_library(confer_tester)
target_compile_features(confer_tester PUBLIC cxx_std_23)
target_sources(confer_tester PRIVATE ${CONFER_TESTER_SOURCES})
target_sources(confer_tester PUBLIC
    FILE_SET HEADERS
    BASE_DIRS ${CONFER_TESTER_INCLUDE_DIRS}
    FILES ${CONFER_TESTER_HEADERS}
)

if(CONFER_TESTER_BUILD_TESTS)
    add_subdirectory(tests)
endif()

if(CONFER_TESTER_BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/confer_tester_config_version.cmake"
    COMPATIBILITY AnyNewerVersion
)

install(
    FILES "${CMAKE_CURRENT_BINARY_DIR}/confer_tester_config_version.cmake"
    DESTINATION "${CMAKE_INSTALL_DATADIR}/confer_tester"
)
install(
    FILES "${CMAKE_CURRENT_BINARY_DIR}/confer_tester.pc"
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/pkgconfig"
)
install(
    TARGETS confer_tester
    EXPORT confer_tester_targets
    FILE_SET HEADERS
)
install(
    EXPORT confer_tester_targets
    NAMESPACE confer_tester::
    DESTINATION "${CMAKE_INSTALL_DATADIR}/confer_tester"
)

find_package(Doxygen REQUIRED)

add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/doc
    COMMAND "${DOXYGEN_EXECUTABLE}" "${CMAKE_CURRENT_BINARY_DIR}/Doxyfile"
    VERBATIM
)

add_custom_target(doc
    DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/doc
)

# Taken from GLFW
# Only generate this target if no higher-level project already has
if (NOT TARGET uninstall)
    configure_file(
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake/cmake_uninstall.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
        IMMEDIATE @ONLY
    )

    add_custom_target(uninstall
        "${CMAKE_COMMAND}" -P
        "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    )
endif()
