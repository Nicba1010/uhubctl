cmake_minimum_required(VERSION 3.13.4)

project(
        uhbctl
        VERSION 2.4.0
        DESCRIPTION "USB hub per-port power control"
        HOMEPAGE_URL "https://github.com/mvp/uhubctl"
        LANGUAGES CXX C
)

set(CMAKE_C_STANDARD 99)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake;${CMAKE_MODULE_PATH}")

find_package(libusb-1.0 REQUIRED)

add_executable(
        uhbctl
        uhubctl.c
)

target_compile_definitions(
        uhbctl
        PRIVATE
        PROGRAM_VERSION="${PROJECT_VERSION}"
)

target_link_libraries(
        uhbctl
        PRIVATE
        ${LIBUSB_1_LIBRARIES}
)

target_include_directories(
        uhbctl
        PRIVATE
        ${LIBUSB_1_INCLUDE_DIRS}
)

install(
        TARGETS
        uhbctl
        DESTINATION
        /usr/sbin
)

set(CPACK_GENERATOR "DEB")

set(CPACK_DEBIAN_COMPRESSION_TYPE "gzip")
set(CPACK_PACKAGE_VENDOR "mvp")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION ${PROJECT_DESCRIPTION})
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Ubuntu MOTU Developers @ ubuntu-motu@lists.ubuntu.com")