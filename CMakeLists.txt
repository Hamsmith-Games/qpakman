cmake_minimum_required(VERSION 2.6)

project(QPAKMAN CXX)

find_package(PNG REQUIRED)

add_definitions(${PNG_DEFINITIONS})
include_directories(${PNG_INCLUDE_DIRS} ${ZLIB_INCLUDE_DIRS})

if(UNIX)
	add_definitions(-DUNIX)
elseif(WIN32)
	add_definitions(-DWIN32)
else()
	message(SEND_ERROR "You are building on unsupported platform")
endif()

file(GLOB SRC_FILES "src/*.cc")

add_executable(qpakman ${SRC_FILES})

set_property(TARGET qpakman PROPERTY COMPILE_FLAGS -fno-rtti)

target_link_libraries(qpakman m ${PNG_LIBRARIES})

install(TARGETS qpakman RUNTIME DESTINATION bin)
