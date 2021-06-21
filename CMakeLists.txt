cmake_minimum_required(VERSION 3.9)

project(sljit C CXX)

set(CMAKE_CXX_STANDARD 11)

function(add_sljit_flags)
  cmake_parse_arguments(ADD_SLJIT "" "" "" ${ARGN})
  foreach(_target ${ADD_SLJIT_UNPARSED_ARGUMENTS})
    target_include_directories(${_target} PUBLIC "${CMAKE_SOURCE_DIR}/sljit_src")
    target_link_options(${_target} PUBLIC -lm -lpthread)
    set_target_properties(${_target} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
  endforeach()
endfunction(add_sljit_flags)

execute_process(COMMAND ${CMAKE_COMMAND} "-E" "create_symlink" "${CMAKE_SOURCE_DIR}" "${CMAKE_BINARY_DIR}/src_dir")

add_library(sljitLir OBJECT sljit_src/sljitLir.c)

add_library(sljitMain OBJECT test_src/sljitMain.c)
target_include_directories(sljitMain PUBLIC "${CMAKE_SOURCE_DIR}/sljit_src")

add_executable(sljit_test test_src/sljitTest.c sljit_src/sljitLir.c $<TARGET_OBJECTS:sljitMain>)
target_include_directories(sljit_test PUBLIC "${CMAKE_SOURCE_DIR}/test_src")
target_compile_options(sljit_test BEFORE PUBLIC "-DSLJIT_HAVE_CONFIG_PRE=1")
add_sljit_flags(sljit_test)

add_library(regexMain OBJECT regex_src/regexMain.c)
target_include_directories(regexMain PUBLIC "${CMAKE_SOURCE_DIR}/sljit_src")
target_compile_options(regexMain PUBLIC "-fshort-wchar")

add_library(regexJIT OBJECT regex_src/regexJIT.c)
target_include_directories(regexJIT PUBLIC "${CMAKE_SOURCE_DIR}/sljit_src")
target_compile_options(regexJIT PUBLIC "-fshort-wchar")

add_executable(regex_test $<TARGET_OBJECTS:regexMain> $<TARGET_OBJECTS:regexJIT> $<TARGET_OBJECTS:sljitLir>)
add_sljit_flags(regex_test)

add_executable(func_call doc/tutorial/func_call.c $<TARGET_OBJECTS:sljitLir>)

add_executable(first_program doc/tutorial/first_program.c $<TARGET_OBJECTS:sljitLir>)

add_executable(branch doc/tutorial/branch.c $<TARGET_OBJECTS:sljitLir>)

add_executable(loop doc/tutorial/loop.c $<TARGET_OBJECTS:sljitLir>)

add_executable(array_access doc/tutorial/array_access.c $<TARGET_OBJECTS:sljitLir>)

add_executable(struct_access doc/tutorial/struct_access.c $<TARGET_OBJECTS:sljitLir>)

add_executable(temp_var doc/tutorial/temp_var.c $<TARGET_OBJECTS:sljitLir>)

add_executable(brainfuck doc/tutorial/brainfuck.c $<TARGET_OBJECTS:sljitLir>)

add_sljit_flags(func_call first_program branch loop array_access struct_access temp_var brainfuck)
