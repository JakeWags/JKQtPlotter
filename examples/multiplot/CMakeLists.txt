cmake_minimum_required(VERSION 3.16)

set(EXAMPLE_NAME multiplot)
set(EXENAME jkqtptest_${EXAMPLE_NAME})

message( STATUS "..   Building Example ${EXAMPLE_NAME}" )


# Set up source files
set(SOURCES test_multiplot.cpp test_multiplot_ui.cpp)
set(HEADERS test_multiplot_ui.h)
set(RESOURCES test_multiplot.qrc )
set(UIS test_multiplot_ui.ui )

add_executable(${EXENAME} WIN32 ${SOURCES} ${HEADERS} ${RESOURCES} ${UIS})
target_link_libraries(${EXENAME} JKQTPExampleToolsLib)
target_include_directories(${EXENAME} PRIVATE ../../lib)
if(JKQtPlotter_BUILD_STATIC_LIBS)
    target_link_libraries(${EXENAME} JKQTPlotterLib)

elseif(JKQtPlotter_BUILD_SHARED_LIBS)
    target_link_libraries(${EXENAME} JKQTPlotterSharedLib)

endif()

# precomiled headers to speed up compilation
if (JKQtPlotter_BUILD_WITH_PRECOMPILED_HEADERS)
  target_precompile_headers(${EXENAME} REUSE_FROM jkqtptest_simpletest)
endif (JKQtPlotter_BUILD_WITH_PRECOMPILED_HEADERS)


# Installation
install(TARGETS ${EXENAME} RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

#Installation of Qt DLLs on Windows
jkqtplotter_deployqt(${EXENAME})
