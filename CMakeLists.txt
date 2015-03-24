project(game.libretro.tgbdual)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

include(ExternalProject)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

externalproject_add(tgbdual
                    GIT_REPOSITORY https://github.com/libretro/tgbdual-libretro
                    GIT_TAG ea1364c
                    PREFIX tgbdual
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(TGBDUAL_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/tgbdual/src/tgbdual/tgbdual_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                          game.libretro.tgbdual${CMAKE_SHARED_LIBRARY_SUFFIX} tgbdual)

build_addon(game.libretro.tgbdual TGBDUAL DEPLIBS)
add_dependencies(game.libretro.tgbdual tgbdual)

include(CPack)
