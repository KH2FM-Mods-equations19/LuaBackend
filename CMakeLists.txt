cmake_minimum_required(VERSION 3.13)

project(LuaBackendHook)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# LuaBackendLIB

add_library(LuaBackendLIB STATIC
    LuaBackendLIB/source/DCInstance.cpp
    LuaBackendLIB/source/GitRequest.cpp
    LuaBackendLIB/source/LuaBackend.cpp
)

target_include_directories(LuaBackendLIB PUBLIC
    LuaBackendLIB/include
    LuaBackendLIB/include/lua
    LuaBackendLIB/include/discord
)

target_link_directories(LuaBackendLIB PUBLIC
    LuaBackendLIB/libraries/lua
    LuaBackendLIB/libraries/discord
)

target_link_libraries(LuaBackendLIB PUBLIC lua54.lib PUBLIC discord-rpc.lib)

target_compile_definitions(LuaBackendLIB PRIVATE -DUNICODE -D_UNICODE)

# DBGHELP

add_library(DBGHELP SHARED LuaBackendDLL/main_dll.cpp)

target_compile_definitions(DBGHELP PRIVATE -DUNICODE -D_UNICODE)

target_link_libraries(DBGHELP LuaBackendLIB)
