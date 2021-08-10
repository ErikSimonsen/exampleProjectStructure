add_executable(Tests test.cpp)
target_link_libraries(
  Tests
  gtest_main
)
include(GoogleTest)
gtest_discover_tests(Tests)