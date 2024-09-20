cmake_minimum_required(VERSION 3.19)
project(png-usage)

if(POLICY CMP0077)
  # Allow CMake 3.13+ to override options when using FetchContent / add_subdirectory.
  cmake_policy(SET CMP0077 NEW)
endif()

# more logging from FetchContent
set(FETCHCONTENT_QUIET OFF)

include(FetchContent)

FetchContent_Declare(
  zlib_repo
  GIT_REPOSITORY "https://github.com/madler/zlib"
)
FetchContent_MakeAvailable(zlib_repo)

# app_zlib
add_executable(app_zlib app_z.cpp)
target_link_libraries(app_zlib zlib)

FetchContent_Declare(
  libpng
  GIT_REPOSITORY "https://github.com/glennrp/libpng.git"
)
set(PNG_TESTS OFF)
FetchContent_MakeAvailable(libpng)


# app_png 
add_executable(app_png app_png.cpp)
target_link_libraries(app_png png_static)
