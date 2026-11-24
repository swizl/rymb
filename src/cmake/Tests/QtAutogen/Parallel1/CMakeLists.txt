cmake_minimum_required(VERSION 3.16)
project(Parallel1)
include("../AutogenGuiTest.配置脚本")

# Test different values for AUTOGEN_PARALLEL
include("../Parallel/parallel.配置脚本")

add_executable(parallel1 ${PARALLEL_SRC})
set_target_properties(parallel1 PROPERTIES AUTOGEN_PARALLEL 1)
target_link_libraries(parallel1 ${QT_LIBRARIES})
