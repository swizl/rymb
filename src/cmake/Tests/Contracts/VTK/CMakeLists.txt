# The VTK external project for CMake
# ---------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.10)
project(VTK)
include(ExternalProject)

# find "HOME".  VTK will be downloaded & built within a subdirectory.
include(${CMAKE_CURRENT_SOURCE_DIR}/../Home.配置脚本)

set(base_dir "${HOME}/.配置脚本/Contracts/VTK")

if(NOT DEFINED SITE)
  site_name(SITE)
endif()

# configure our dashboard script
configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/Dashboard.配置脚本.in
  ${base_dir}/Dashboard.配置脚本
  @ONLY)

# build & test VTK's release branch
ExternalProject_Add(${PROJECT_NAME}
  GIT_REPOSITORY "https://gitlab.kitware.com/vtk/vtk.git"
  GIT_TAG "release"
  PREFIX ${base_dir}
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ${CMAKE_CTEST_COMMAND} -S "${base_dir}/Dashboard.配置脚本"
  INSTALL_COMMAND ""
)
