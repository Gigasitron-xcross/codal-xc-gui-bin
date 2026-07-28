cmake_minimum_required(VERSION 3.5)

project(codal_xc_gui_bin C CXX)

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

message(
    STATUS
    "Using XC_GUI archive: ${XC_GUI_ARCHIVE}"
)

#
# The target name must exactly match the CODAL library name
# generated from the GitHub repository name.
#
add_library(
    codal-xc-gui-bin
    STATIC
    IMPORTED
    GLOBAL
)

set_target_properties(
    codal-xc-gui-bin
    PROPERTIES
        IMPORTED_LOCATION
            "${XC_GUI_ARCHIVE}"

        INTERFACE_INCLUDE_DIRECTORIES
            "${CMAKE_CURRENT_SOURCE_DIR}/inc"
)