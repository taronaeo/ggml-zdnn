#
# perf-zdnn

set(TEST_TARGET perf-zdnn)
add_executable(${TEST_TARGET} perf-zdnn.cpp)
target_link_libraries(${TEST_TARGET} PRIVATE ggml)
