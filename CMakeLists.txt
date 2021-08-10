cmake_minimum_required(VERSION 3.14)
project(Practice)

# GoogleTest requires at least C++11
set(CMAKE_CXX_STANDARD 17)

if (MSVC)
    # warning level 4 and all warnings as errors
    add_compile_options(/W4 /WX)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()

# Download GoogleTest as a Dependency on each build
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# no including of CTest necessary as it is automatically used if the usage of GoogleTests is detected (/tests/CMakeLists.txt)
# CTest allows execution of all tests at once (even it they are in multiple files)
enable_testing()

# Add the given directories to those the compiler uses to search for includes. Otherwise the tests can't find the classes that need to be tested
include_directories(src)
# Add both CMakeLists.txt which each produce a executable. The one in /tests first links the executable to the google test library (see /tests/CMakeLists.txt)
add_subdirectory(tests)
add_subdirectory(src)