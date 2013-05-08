# CMake build for CompilerRT.
#
project(c++abi)
# The CompilerRT build system requires CMake version 2.8.8 or higher in order
# to use its support for building convenience "libraries" as a collection of
# .o files. This is particularly useful in producing larger, more complex
# runtime libraries.
cmake_minimum_required(VERSION 2.8.8)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -stdlib=libc++ -fstrict-aliasing -Wstrict-aliasing=2")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wsign-conversion -Wshadow -Wconversion -Wunused-variable")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wmissing-field-initializers -Wchar-subscripts -Wmismatched-tags")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wmissing-braces -Wshorten-64-to-32 -Wsign-compare")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wstrict-aliasing=2 -Wstrict-overflow=4 -Wunused-parameter")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wnewline-eof")


option(LIBCXX_ENABLE_SHARED "Build libc++abi as a shared library." ON)


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
if (LIBCXX_ENABLE_SHARED)
 add_library(c++abi-shared SHARED ${GENERIC_SOURCES})
 set_target_properties(c++abi-shared PROPERTIES
                      OUTPUT_NAME "c++abi"
                     )
  install(TARGETS c++abi-shared
    LIBRARY DESTINATION lib
  )
else(LIBCXX_ENABLE_SHARED)
  add_library(c++abi-static STATIC ${GENERIC_SOURCES})
  set_target_properties(c++abi-static PROPERTIES
                      OUTPUT_NAME "c++abi"
                     )


  install(TARGETS c++abi-static
    ARCHIVE DESTINATION lib
  )
endif(LIBCXX_ENABLE_SHARED)