set(LLVM_LINK_COMPONENTS
  ${LLVM_TARGETS_TO_BUILD}
  BitReader
  Core
  MCDisassembler
  Object
  Target
  )

if(TARGET LLVM)
  set(LLVM_LINK_COMPONENTS)
endif()

if (LLVM_COMPILER_IS_GCC_COMPATIBLE)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu99 -Wstrict-prototypes")
endif ()

add_llvm_tool(llvm-c-test
  calc.c
  disassemble.c
  helpers.c
  include-all.c
  main.c
  module.c
  object.c
  targets.c
  )

# Use libLLVM.so if it is available.
if(TARGET LLVM)
  target_link_libraries(llvm-c-test LLVM)
endif()
