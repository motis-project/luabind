cmake_minimum_required(VERSION 3.16)
project(lua)

find_package(Boost REQUIRED)

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
target_link_libraries(luabind lua)
target_include_directories(luabind SYSTEM PUBLIC . ${Boost_INCLUDE_DIR})
