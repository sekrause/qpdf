
# CMake instructions to test using the static lib

SET( APP_EXE qpdf )

ADD_EXECUTABLE(qpdf-static qpdf.cc)

TARGET_LINK_LIBRARIES(qpdf-static libqpdf-static ${JPEG_LIBRARIES} ZLIB::ZLIB)

ADD_EXECUTABLE( test_driver test_driver.cc )
TARGET_LINK_LIBRARIES(test_driver libqpdf)

#set_property(TARGET qpdf-static PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

set_target_properties(
	qpdf-static test_driver
	PROPERTIES
	MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"
)
