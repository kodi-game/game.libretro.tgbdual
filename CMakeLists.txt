cmake_minimum_required(VERSION 3.1)
project(game.libretro.tgbdual)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_library(TGBDUAL_LIB NAMES tgbdual_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} PATH_SUFFIXES libretro)

set(TGBDUAL_CUSTOM_BINARY ${TGBDUAL_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} TGBDUAL "")

include(CPack)
