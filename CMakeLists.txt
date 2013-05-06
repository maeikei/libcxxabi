# CMake build for CompilerRT.
#
project(c++abi)
# The CompilerRT build system requires CMake version 2.8.8 or higher in order
# to use its support for building convenience "libraries" as a collection of
# .o files. This is particularly useful in producing larger, more complex
# runtime libraries.
cmake_minimum_required(VERSION 2.8.8)


set(GENERIC_SOURCES

src/abort_message.cpp
src/abort_message.h
src/cxa_aux_runtime.cpp
src/cxa_default_handlers.cpp
src/cxa_demangle.cpp
src/cxa_exception.cpp
src/cxa_exception.hpp
src/cxa_exception_storage.cpp
src/cxa_guard.cpp
src/cxa_handlers.cpp
src/cxa_handlers.hpp
src/cxa_new_delete.cpp
src/cxa_personality.cpp
src/cxa_unexpected.cpp
src/cxa_vector.cpp
src/cxa_virtual.cpp
src/exception.cpp
src/fallback_malloc.ipp
src/private_typeinfo.cpp
src/private_typeinfo.h
src/stdexcept.cpp
src/typeinfo.cpp

  )
add_library(c++abi-static STATIC ${GENERIC_SOURCES})
set_target_properties(c++abi-static PROPERTIES
                      OUTPUT_NAME "c++abi"
                     )

install(TARGETS c++abi-static
  ARCHIVE DESTINATION lib
  )
