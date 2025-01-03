set(CONFER_TESTER_EXAMPLES
    "example"
)

function(add_example source executable)
    add_executable(${executable} ${source})
    target_link_libraries(${executable} confer_tester)
endfunction()

foreach(example ${CONFER_TESTER_EXAMPLES})
    set(example_source "${CMAKE_CURRENT_SOURCE_DIR}/${example}.cpp")
    string(REPLACE "/" "_" example_executable confer_tester_${example})
    add_example(${example_source} ${example_executable})
endforeach()
