if(NOT(LLVM_LIBC_FULL_BUILD))
  # in overlay mode, use the system's file to test the reader.
  set(use_system_file "-DLIBC_COPT_STDIO_USE_SYSTEM_FILE")
endif()

add_libc_unittest(
  parser_test
  SUITE
    libc_stdio_unittests
  SRCS
    parser_test.cpp
  LINK_LIBRARIES
    LibcScanfHelpers
  DEPENDS
    libc.src.stdio.scanf_core.parser
    libc.src.stdio.scanf_core.core_structs
    libc.src.__support.CPP.string_view
    libc.src.__support.arg_list
)

add_libc_unittest(
  reader_test
  SUITE
    libc_stdio_unittests
  SRCS
    reader_test.cpp
  DEPENDS
    libc.src.stdio.scanf_core.reader
    libc.src.__support.CPP.string_view
  COMPILE_OPTIONS
    ${use_system_file}
)

add_libc_unittest(
  converter_test
  SUITE
    libc_stdio_unittests
  SRCS
    converter_test.cpp
  DEPENDS
    libc.src.stdio.scanf_core.reader
    libc.src.stdio.scanf_core.converter
    libc.src.__support.CPP.string_view
  COMPILE_OPTIONS
    ${use_system_file}
)
