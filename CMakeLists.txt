cmake_minimum_required(VERSION 3.7)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Don't bother writing the project name all the time:
set(PROJECT dhcpoptinj)

project(
	${PROJECT}
	VERSION 0.5.4
	DESCRIPTION "DHCP option injector"
	LANGUAGES C
	)

set(CMAKE_C_STANDARD 99)

add_definitions(-DDHCPOPTINJ_VERSION="${PROJECT_VERSION}")

set(SOURCES
	src/config.c
	src/dhcp.c
	src/dhcpoptinj.c
	src/ipv4.c
	src/options.c
	)

set(HEADERS
	src/config.h
	src/dhcp.h
	src/ipv4.h
	src/options.h
	src/udp.h
	)

add_executable(${PROJECT} ${SOURCES} ${HEADERS})

find_library(NFQ_LIB netfilter_queue REQUIRED)
target_link_libraries(${PROJECT} ${NFQ_LIB})

install(TARGETS ${PROJECT} DESTINATION bin)
