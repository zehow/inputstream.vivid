cmake_minimum_required(VERSION 3.16)
project(inputstream.vivid)

set(ADDON_ID inputstream.vivid)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# 修复晶晨硬解编译报错
add_compile_options(-fpermissive -w)

# ==============================================
# 🔥 Kodi 21 (Omega) 正确头文件路径
# ==============================================
# Kodi 21 的头文件在 xbmc 目录下，而不是 kodi-addon-kit
include_directories(
    ${KODI_SOURCE_DIR}/xbmc
    ${KODI_SOURCE_DIR}/xbmc/addons
    ${KODI_SOURCE_DIR}/xbmc/cores/VideoPlayer
    src
)

# 如果上面不行，尝试使用 kodi-addon-kit 的备用路径
# include_directories(${KODI_SOURCE_DIR}/xbmc/addons/kodi-addon-kit/include)

# 自动搜索源码
file(GLOB_RECURSE SOURCES src/*.cpp)

# 编译插件
add_library(${ADDON_ID} SHARED ${SOURCES})
set_target_properties(${ADDON_ID} PROPERTIES PREFIX "")

# 系统依赖
target_link_libraries(${ADDON_ID} pthread dl)
