set(CONFER_TESTER_TESTS
    "${CMAKE_CURRENT_SOURCE_DIR}/test.cpp"
)

add_executable(confer_tester_tester ${CONFER_TESTER_TESTS})
target_include_directories(confer_tester_tester PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}/test_ap")
target_link_libraries(confer_tester_tester PRIVATE confer_tester)
