cmake_minimum_required(VERSION 3.16)
project(lua)

if(IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/deps")
  add_subdirectory(deps)
endif()

set(SOURCES
  src/class.cpp
  src/class_info.cpp
  src/class_registry.cpp
  src/class_rep.cpp
  src/create_class.cpp
  src/error.cpp
  src/exception_handler.cpp
  src/function.cpp
  src/inheritance.cpp
  src/link_compatibility.cpp
  src/object_rep.cpp
  src/open.cpp
  src/pcall.cpp
  src/scope.cpp
  src/stack_content_by_name.cpp
  src/weak_ref.cpp
  src/wrapper_base.cpp
)
add_library(luabind STATIC ${SOURCES})
target_compile_features(luabind PRIVATE cxx_std_14)
target_link_libraries(luabind lua boost)
target_include_directories(luabind SYSTEM PUBLIC .)
if (NOT MSVC)
  target_compile_options(luabind PRIVATE -Wno-deprecated-declarations)
endif ()

if (CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
  target_compile_definitions(luabind PUBLIC _LIBCPP_ENABLE_CXX17_REMOVED_AUTO_PTR=1)
  endif()
if (MSVC)
  target_compile_definitions(luabind PUBLIC _HAS_AUTO_PTR_ETC=1)
endif()
