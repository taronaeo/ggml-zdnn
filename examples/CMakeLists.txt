if (GGML_ALL_WARNINGS)
  if (NOT MSVC)
      set(cxx_flags
          # TODO(marella): Add other warnings.
          -Wpedantic
          -Wunused-variable
          -Wno-unused-function
          -Wno-multichar
      )
      add_compile_options("$<$<COMPILE_LANGUAGE:CXX>:${cxx_flags}>")
  endif()
endif()

add_library(common STATIC common.cpp)
target_include_directories(common PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

add_library(common-ggml STATIC common-ggml.cpp)
target_link_libraries(common-ggml PRIVATE ggml)
target_include_directories(common-ggml PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

add_subdirectory(yolo)

if (NOT GGML_BACKEND_DL)
    add_subdirectory(gpt-2)
    add_subdirectory(gpt-j)
    add_subdirectory(mnist)
    add_subdirectory(sam)
    add_subdirectory(simple)
    add_subdirectory(magika)
endif()

if (GGML_METAL)
    add_subdirectory(perf-metal)
endif()

if (GGML_ZDNN)
    add_subdirectory(perf-zdnn)
endif()
