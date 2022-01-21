cmake_minimum_required( VERSION 3.15 )

project( "simple-boost-serial-port"
    VERSION 1.11
    DESCRIPTION "A set of C++ classes to easily handle serial ports across different platforms, built on top of boost.asio"
)

find_package( Boost 1.40.0 REQUIRED )

set( THREADS_PREFER_PTHREAD_FLAG ON )
find_package( Threads REQUIRED )

set( CMAKE_CXX_STANDARD 11 )

add_library( ${PROJECT_NAME}
	src/TimeoutSerial.cpp
	src/SerialStream.cpp
	src/BufferedAsyncSerial.cpp
	src/AsyncSerial.cpp
	src/SimpleSerial.cpp
)

target_include_directories( ${PROJECT_NAME}
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
	${Boost_INCLUDE_DIR}
)

target_link_libraries( ${PROJECT_NAME}
    PRIVATE
        ${Boost_LIBRARIES}
	${CMAKE_THREAD_LIBS_INIT}
)

add_executable(
	1_simple 
	examples/1_simple/main.cpp
)

target_link_libraries(1_simple ${PROJECT_NAME})

add_executable(
	2_with_timeout 
	examples/2_with_timeout/main.cpp
)

target_link_libraries(2_with_timeout ${PROJECT_NAME})

add_executable(
	3_async 
	examples/3_async/main.cpp
)

target_link_libraries(3_async ${PROJECT_NAME})

add_executable(
	4_callback_simple
	examples/4_callback/main.cpp
)

target_link_libraries(4_callback_simple ${PROJECT_NAME})

add_executable(
	4_callback_termios
	examples/4_callback/test.cpp
)

target_link_libraries(4_callback_termios ${PROJECT_NAME})

add_executable(
	6_stream
	examples/6_stream/main.cpp
)

target_link_libraries(6_stream ${PROJECT_NAME})





