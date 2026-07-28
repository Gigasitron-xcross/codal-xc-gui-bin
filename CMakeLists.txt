include("${CODAL_UTILS_LOCATION}")

RECURSIVE_FIND_DIR(
    INCLUDE_DIRS
    "${CMAKE_CURRENT_SOURCE_DIR}/inc"
    "*.h"
)

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
    "XC_GUI archive: ${XC_GUI_ARCHIVE}"
)

add_library(
    codal-xc-gui-bin
    STATIC
    "${CMAKE_CURRENT_SOURCE_DIR}/source/xc_gui_bin_anchor.cpp"
)

target_include_directories(
    codal-xc-gui-bin
    PUBLIC
        ${INCLUDE_DIRS}
)

target_link_libraries(
    codal-xc-gui-bin
    PUBLIC
        "${XC_GUI_ARCHIVE}"
)