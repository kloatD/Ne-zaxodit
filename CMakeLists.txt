cmake_minimum_required(VERSION 3.20)
project(stealer CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

add_executable(stealer WIN32 main.cpp)

find_package(CURL REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(unofficial-sqlite3 CONFIG REQUIRED)

target_link_libraries(stealer PRIVATE
    CURL::libcurl
    OpenSSL::SSL
    OpenSSL::Crypto
    unofficial::sqlite3::sqlite3
    crypt32 bcrypt ws2_32 gdiplus shlwapi advapi32 user32
)

target_compile_options(stealer PRIVATE /O2 /Gy /Gs- /MT /utf-8)
set_property(TARGET stealer PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded")
