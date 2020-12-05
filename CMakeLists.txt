cmake_minimum_required(VERSION 3.16)
cmake_policy(SET CMP0076 NEW)
cmake_policy(SET CMP0091 NEW)

project(tgcalls
        DESCRIPTION "Python binding for tgcalls"
        HOMEPAGE_URL "https://github.com/tgcalls"
)

get_filename_component(third_party_loc "tgcalls/third_party" REALPATH)
get_filename_component(src_loc "tgcalls/src" REALPATH)

include(cmake/variables.cmake)
if (build_win64)
    get_filename_component(libs_loc "./Libraries/win64" REALPATH)
elseif (NOT APPLE OR build_osx)
    get_filename_component(libs_loc "./Libraries" REALPATH)
else()
    get_filename_component(libs_loc "./Libraries/macos" REALPATH)
endif()

include(cmake/nice_target_sources.cmake)
include(cmake/target_link_frameworks.cmake)
include(cmake/options.cmake)
include(cmake/init_target.cmake)

add_subdirectory(cmake/external/openssl)
add_subdirectory(cmake/external/jpeg)
add_subdirectory(cmake/external/opus)
add_subdirectory(cmake/external/webrtc)

add_subdirectory(tgcalls)