cmake_minimum_required(VERSION 3.16)
project(UicOnly)
include("../AutogenGuiTest.配置脚本")

# Test AUTOUIC being enabled only
add_executable(uicOnly main.cpp UicOnly.cpp)
set_property(TARGET uicOnly PROPERTY AUTOUIC ON)
target_link_libraries(uicOnly ${QT_LIBRARIES})
