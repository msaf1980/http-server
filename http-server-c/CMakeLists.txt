cmake_minimum_required( VERSION 3.5 )

project( http_server )

set( DIR_SOURCES src )
set( DIR_INCLUDES includes )
set( DIR_TESTS test )


# Be nice to visual studio
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Be nice and export compile commands by default, this is handy for clang-tidy and for other tools.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)


if ( DEFINED DIR_INCLUDES AND IS_DIRECTORY ${DIR_INCLUDES} )
    # Includes in separate directory
    include_directories( include )
endif()

#Scan dir for standart source files
aux_source_directory( ${DIR_SOURCES} SOURCES )

# Add executable target
add_executable( http_server ${SOURCES} )

if ( DEFINED DIR_TESTS )
    #set enable testing
    enable_testing()
    foreach ( dir IN LISTS DIR_TESTS )
        if ( IS_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/${dir} )
            message("test dir ${dir}")
            add_subdirectory( ${dir} )
        endif()
    endforeach()
endif()
