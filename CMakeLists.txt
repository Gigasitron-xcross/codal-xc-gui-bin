project(codal-xc-gui-bin)

include("${CODAL_UTILS_LOCATION}")

set(
    XC_GUI_ARCHIVE
    "${CMAKE_CURRENT_SOURCE_DIR}/lib/microbit-v2/libXC_GUI.a"
)

if(NOT EXISTS "${XC_GUI_ARCHIVE}")
    message(
        FATAL_ERROR
        "XC_GUI archive not found: ${XC_GUI_ARCHIVE}"
    )
endif()

#
# The target name must match the CODAL library/repository name:
#
#     codal-xc-gui-bin
#
# PXT/CODAL will link this target into MICROBIT.
#
add_library(
    xc-gui-prebuilt
    STATIC
    IMPORTED
    GLOBAL
)

set_target_properties(
    xc-gui-prebuilt
    PROPERTIES
        IMPORTED_LOCATION
            "${XC_GUI_ARCHIVE}"
)

add_library(
    codal-xc-gui-bin
    INTERFACE
)

target_include_directories(
    codal-xc-gui-bin
    INTERFACE
        "${CMAKE_CURRENT_SOURCE_DIR}/inc"
)

target_link_libraries(
    codal-xc-gui-bin
    INTERFACE
        xc-gui-prebuilt
)