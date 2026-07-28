project(codal-xc-gui)

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

add_library(
    xc_gui_prebuilt
    STATIC
    IMPORTED
    GLOBAL
)

set_target_properties(
    xc_gui_prebuilt
    PROPERTIES
    IMPORTED_LOCATION "${XC_GUI_ARCHIVE}"
)

add_library(
    codal-xc-gui
    INTERFACE
)

target_include_directories(
    codal-xc-gui
    INTERFACE
    "${CMAKE_CURRENT_SOURCE_DIR}/inc"
)

target_link_libraries(
    codal-xc-gui
    INTERFACE
    xc_gui_prebuilt
)

# Make headers visible to xcgui.cpp and LCD_ST7789_Port.cpp.
include_directories(
    "${CMAKE_CURRENT_SOURCE_DIR}/inc"
)