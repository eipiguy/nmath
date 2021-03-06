# ./CMakeLists.txt
cmake_minimum_required( VERSION 3.15 )

# load meta information
include( "${CMAKE_CURRENT_SOURCE_DIR}/project_meta_info.in" )
project( nmath
    VERSION         ${project_version}
    DESCRIPTION     ${project_description}
    HOMEPAGE_URL    ${project_homepage}
    LANGUAGES       ${project_languages}
)

message( "" )
message( "project_version:      ${project_version}" )
message( "project_description:  ${project_description}" )
message( "project_homepage:     ${project_homepage}" )
message( "project_languages:    ${project_languages}" )
message( "" )

# set default binary symbol visibilities to hidden
if( NOT DEFINED CMAKE_CXX_VISIBILITY_PRESET AND
    NOT DEFINED CMAKE_VISIBILITY_INLINES_HIDDEN
)
    set( CMAKE_CXX_VISIBILITY_PRESET        hidden )
    set( CMAKE_VISIBILITY_INLINES_HIDDEN    YES )
endif()

# provided libraries
add_subdirectory( nlinear )

# installation
include( GNUInstallDirs )
install(
    TARGETS nlinear
    EXPORT  nlinear_targets

    INCLUDES    DESTINATION         "${CMAKE_INSTALL_INCLUDEDIR}"

    RUNTIME     DESTINATION         "${CMAKE_INSTALL_BINDIR}"
                COMPONENT           nmath_runtime
    LIBRARY     DESTINATION         "${CMAKE_INSTALL_LIBDIR}"
                COMPONENT           nmath_runtime
                NAMELINK_COMPONENT  nmath_development
    ARCHIVE     DESTINATION         "${CMAKE_INSTALL_LIBDIR}"
                COMPONENT           nmath_development
)