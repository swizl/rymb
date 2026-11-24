cmake_minimum_required(VERSION 3.16)
project(Parallel3)
include("../AutogenGuiTest.配置脚本")

# Test different values for AUTOGEN_PARALLEL
include("../Parallel/parallel.配置脚本")

add_executable(parallel3 ${PARALLEL_SRC})
set_target_properties(parallel3 PROPERTIES AUTOGEN_PARALLEL 3)
target_link_libraries(parallel3 ${QT_LIBRARIES})
