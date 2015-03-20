IF(BIICODE AND (NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/libtest/test.h"))
	# Someone is depending on this library and test files are not a dependency, end build them.
	RETURN()
ENDIF()

add_subdirectory(data)
add_subdirectory(libtest)
add_subdirectory(server)
