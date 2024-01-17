macro( target_link_framework TARGET NAME )
    find_library( FRAMEWORK_${NAME}
        NAMES ${NAME}
        PATHS ${CMAKE_OSX_SYSROOT}/System/Library
        PATH_SUFFIXES Frameworks PrivateFrameworks
        CMAKE_FIND_FRAMEWORK only
        NO_DEFAULT_PATH )
    if( ${FRAMEWORK_${NAME}} STREQUAL FRAMEWORK_${NAME}-NOTFOUND)
        message( ERROR ": Framework ${NAME} not found" )
    else()
        target_link_libraries( ${TARGET} PUBLIC "${FRAMEWORK_${NAME}}" )
        message( STATUS "Framework ${NAME} found at ${FRAMEWORK_${NAME}}" )
    endif()
endmacro( target_link_framework )


set( SOURCE_FILES
         main.c
         parse.c
         mach.c
         hashtable.c
         events.c
         windows.c
         border.c )

add_executable( borders ${SOURCE_FILES} )
target_include_directories( borders PRIVATE ${CMAKE_CURRENT_LIST_DIR} ${CMAKE_CURRENT_LIST_DIR}/misc )
target_link_framework( borders AppKit )
target_link_framework( borders SkyLight )

