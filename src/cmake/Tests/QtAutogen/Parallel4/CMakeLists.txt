cmake_minimum_required(VERSION 3.16)
project(Parallel4)
include("../AutogenGuiTest.配置脚本")

# Test different values for AUTOGEN_PARALLEL
include("../Parallel/parallel.配置脚本")

add_executable(parallel4 ${PARALLEL_SRC})
set_target_properties(parallel4 PROPERTIES AUTOGEN_PARALLEL 4)
target_link_libraries(parallel4 ${QT_LIBRARIES})
