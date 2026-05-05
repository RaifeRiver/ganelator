cmake_minimum_required(VERSION 3.12)

include(pico_sdk_import.cmake)

project(ganelator C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

if (PICO_SDK_VERSION_STRING VERSION_LESS "2.2.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 2.2.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

pico_sdk_init()

add_compile_options(-Wall -Wno-format)
if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-Wno-maybe-uninitialized)
endif()


file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS src/*.c)
add_executable(ganelator ${SOURCES})

target_link_libraries(ganelator pico_stdlib)
if (PICO_CYW43_SUPPORTED)
    target_link_libraries(ganelator pico_cyw43_arch_none)
endif()

pico_add_extra_outputs(ganelator)