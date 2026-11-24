configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Test.配置脚本.in
               ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本 @ONLY)

macro(add_CMakeOnly_test test)
  add_test(CMakeOnly.${test} ${CMAKE_CMAKE_COMMAND}
    -DTEST=${test}
    -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
    )
endmacro()

add_CMakeOnly_test(LinkInterfaceLoop)
# If a bug is introduced in CMake that causes an infinite loop while
# analyzing LinkInterfaceLoop then don't let the test run too long.
# Use an option to customize it so that the timeout can be extended
# on busy machines.
if(NOT DEFINED CMake_TEST_CMakeOnly.LinkInterfaceLoop_TIMEOUT)
  set(CMake_TEST_CMakeOnly.LinkInterfaceLoop_TIMEOUT 90)
endif()
set_property(TEST CMakeOnly.LinkInterfaceLoop PROPERTY TIMEOUT ${CMake_TEST_CMakeOnly.LinkInterfaceLoop_TIMEOUT})

add_CMakeOnly_test(CheckSymbolExists)

add_CMakeOnly_test(CheckCXXSymbolExists)

add_CMakeOnly_test(CheckCXXCompilerFlag)

add_CMakeOnly_test(CheckLanguage)
set_property(TEST CMakeOnly.CheckLanguage APPEND PROPERTY LABELS "HIP" "Fortran")
if (CMake_TEST_HIP)
  add_CMakeOnly_test(CheckLanguageHIPPlatform)
  set_property(TEST CMakeOnly.CheckLanguageHIPPlatform APPEND PROPERTY LABELS "HIP")
  add_CMakeOnly_test(CheckLanguageHIPPlatform2)
  set_property(TEST CMakeOnly.CheckLanguageHIPPlatform2 APPEND PROPERTY LABELS "HIP")
endif()

add_CMakeOnly_test(CheckStructHasMember)

if (APPLE AND CMAKE_C_COMPILER_ID MATCHES "Clang|GNU")
  add_CMakeOnly_test(CheckOBJCCompilerFlag)
  add_CMakeOnly_test(CheckOBJCXXCompilerFlag)
endif()

add_test(CMakeOnly.AllFindModules ${CMAKE_CMAKE_COMMAND}
  -DTEST=AllFindModules
  -DCMAKE_ARGS=-DCMake_TEST_CMakeOnly.AllFindModules_NO_VERSION=${CMake_TEST_CMakeOnly.AllFindModules_NO_VERSION}
  -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
  )

add_CMakeOnly_test(SelectLibraryConfigurations)

add_CMakeOnly_test(TargetScope)

add_CMakeOnly_test(find_library)
add_CMakeOnly_test(find_path)

add_test(CMakeOnly.ProjectInclude ${CMAKE_CMAKE_COMMAND}
  -DTEST=ProjectInclude
  -DCMAKE_ARGS=-DCMAKE_PROJECT_ProjectInclude_INCLUDE=${CMAKE_CURRENT_SOURCE_DIR}/ProjectInclude/include.配置脚本
  -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
  )

add_test(CMakeOnly.ProjectIncludeAny ${CMAKE_CMAKE_COMMAND}
  -DTEST=ProjectIncludeAny
  -DCMAKE_ARGS=-DCMAKE_PROJECT_INCLUDE=${CMAKE_CURRENT_SOURCE_DIR}/ProjectInclude/include.配置脚本
  -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
  )

add_test(CMakeOnly.ProjectIncludeBefore ${CMAKE_CMAKE_COMMAND}
  -DTEST=ProjectIncludeBefore
  -DCMAKE_ARGS=-DCMAKE_PROJECT_ProjectInclude_INCLUDE_BEFORE=${CMAKE_CURRENT_SOURCE_DIR}/ProjectIncludeBefore/include.配置脚本
  -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
  )

add_test(CMakeOnly.ProjectIncludeBeforeAny ${CMAKE_CMAKE_COMMAND}
  -DTEST=ProjectIncludeBeforeAny
  -DCMAKE_ARGS=-DCMAKE_PROJECT_INCLUDE_BEFORE=${CMAKE_CURRENT_SOURCE_DIR}/ProjectIncludeBefore/include.配置脚本
  -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
  )

include(CMakeParseArguments)

function(add_major_test module)
  cmake_parse_arguments(MAJOR_TEST "NOLANG" "VERSION_VAR" "VERSIONS" ${ARGN})
  foreach (_version IN LISTS MAJOR_TEST_VERSIONS)
    add_test(CMakeOnly.MajorVersionSelection-${module}_${_version}
      ${CMAKE_CMAKE_COMMAND}
        -DTEST=MajorVersionSelection-${module}_${_version}
        -DTEST_SOURCE=MajorVersionSelection
        "-DCMAKE_ARGS=-DMAJOR_TEST_MODULE=${module};-DMAJOR_TEST_VERSION=${_version};-DMAJOR_TEST_NO_LANGUAGES=${MAJOR_TEST_NOLANG};-DMAJOR_TEST_VERSION_VAR=${MAJOR_TEST_VERSION_VAR}"
        -P ${CMAKE_CURRENT_BINARY_DIR}/Test.配置脚本
      )
  endforeach ()
endfunction()

add_major_test(PythonLibs VERSIONS 2 3 VERSION_VAR PYTHONLIBS_VERSION_STRING)
add_major_test(PythonInterp NOLANG VERSIONS 3 VERSION_VAR PYTHON_VERSION_STRING)
add_major_test(Qt VERSIONS 3 4 VERSION_VAR Qt3_VERSION)
