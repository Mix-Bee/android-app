cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ${CMAKE_SOURCE_DIR}/opus)

add_library(lib_opus STATIC IMPORTED)
set_target_properties(lib_opus PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/lib/${ANDROID_ABI}/libopus.a)

add_library(lib_ogg STATIC IMPORTED)
set_target_properties(lib_ogg PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/lib/${ANDROID_ABI}/libogg.a)

add_library(lib_opusenc STATIC IMPORTED)
set_target_properties(lib_opusenc PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/lib/${ANDROID_ABI}/libopusenc.a)

add_library(mixin SHARED
            audio.c
        )

target_include_directories(mixin PRIVATE
                           ${distribution_DIR}/include)

target_link_libraries(mixin
                      android
                      lib_opusenc
                      lib_opus
                      lib_ogg
                      log)