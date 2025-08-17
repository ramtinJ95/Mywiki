## The cmake file

```cmake
cmake_minimum_required(VERSION 3.26)
project(MyProject)

# Export compile commands for clangd / LSP
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Force ccache if available
find_program(CCACHE_PROGRAM ccache)
if(CCACHE_PROGRAM)
    message(STATUS "ccache found: ${CCACHE_PROGRAM}")
    set(CMAKE_CXX_COMPILER_LAUNCHER "${CCACHE_PROGRAM}" CACHE STRING "C++ compiler launcher" FORCE)
    set(CMAKE_C_COMPILER_LAUNCHER "${CCACHE_PROGRAM}" CACHE STRING "C compiler launcher" FORCE)
endif()

# Prefer Clang if available
find_program(CLANGXX clang++)
if(CLANGXX)
    message(STATUS "Clang++ found, using it instead of g++")
    set(CMAKE_CXX_COMPILER ${CLANGXX} CACHE STRING "" FORCE)
endif()

# Source and header directories
set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)
set(INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include)

# Recursively collect all source files in src/
file(GLOB_RECURSE SRC_FILES ${SRC_DIR}/*.cpp)

add_executable(${PROJECT_NAME} ${SRC_FILES})

target_include_directories(${PROJECT_NAME}
    PRIVATE
        ${INCLUDE_DIR}
)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)
target_compile_definitions(${PROJECT_NAME} PRIVATE IMGDIR="../img/")

# Platform-specific compiler options
if(APPLE)
    set(CMAKE_OSX_ARCHITECTURES arm64 CACHE STRING "" FORCE)
    target_compile_options(${PROJECT_NAME} PRIVATE -mcpu=apple-m4)

    # SDL2 paths for macOS (Homebrew, /usr/local)
    list(APPEND CMAKE_MODULE_PATH "/usr/local/lib/cmake/SDL2" "/opt/homebrew/lib/cmake/SDL2")
    list(APPEND CMAKE_PREFIX_PATH "/usr/local" "/opt/homebrew")

elseif(UNIX AND NOT APPLE)
    target_compile_options(${PROJECT_NAME} PRIVATE -march=native)
endif()

# Find SDL2 and SDL2_image
find_package(SDL2 QUIET)
find_package(SDL2_image QUIET)

if (SDL2_FOUND AND SDL2_IMAGE_FOUND)
    message(STATUS "Using SDL2 and SDL2_image from find_package")
    target_include_directories(${PROJECT_NAME} PRIVATE ${SDL2_INCLUDE_DIRS} ${SDL2_IMAGE_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PRIVATE ${SDL2_LIBRARIES} ${SDL2_IMAGE_LIBRARIES})

    # Add rpath only if libs are outside /usr
    if(UNIX AND NOT APPLE)
        foreach(lib_dir ${SDL2_LIBRARY_DIRS} ${SDL2_IMAGE_LIBRARY_DIRS})
            if(NOT lib_dir MATCHES "^/usr(/|$)")
                set_target_properties(${PROJECT_NAME} PROPERTIES
                    BUILD_RPATH "$ORIGIN/../lib"
                    INSTALL_RPATH "$ORIGIN/../lib"
                    INSTALL_RPATH_USE_LINK_PATH TRUE
                )
            endif()
        endforeach()
    endif()

else()
    # Fallback to pkg-config
    find_package(PkgConfig REQUIRED)
    pkg_search_module(SDL2 REQUIRED sdl2)
    pkg_search_module(SDL2_IMAGE REQUIRED SDL2_image)
    message(STATUS "Using SDL2 and SDL2_image from pkg-config")
    target_include_directories(${PROJECT_NAME} PRIVATE ${SDL2_INCLUDE_DIRS} ${SDL2_IMAGE_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PRIVATE ${SDL2_LIBRARIES} ${SDL2_IMAGE_LIBRARIES})
endif()

```

# 🚀 C++ Project Template (CMake + Ninja + Clang + ccache + SDL2)

This is a template for modern C++ projects with **super-fast build times** and **cross-platform support** (Arch Linux + macOS).

---

## ✨ Features
- **CMake 3.26+** build system
- **Ninja** build backend (fast dependency scanning)
- **Clang++** as the default compiler (fast incremental builds, works great with clangd)
- **ccache** enabled automatically (caches object files, near-instant rebuilds)
- **SDL2 + SDL2_image** detection:
  - Uses `find_package` if available
  - Falls back to `pkg-config` on Linux
- **clangd / LSP** support (`compile_commands.json` generated automatically)

---

## ⚡ Why Ninja, Clang, ccache?
- **Ninja**: Much faster than `make` at incremental builds and dependency checks  
- **Clang++**: Generally faster than `g++` for parsing & diagnostics, integrates with `clangd`  
- **ccache**: Avoids recompiling unchanged code — rebuilds drop from seconds to milliseconds  

---

## 🛠️ Setup

### Arch Linux
```bash
sudo pacman -S cmake ninja clang llvm ccache sdl2 sdl2_image
```

### MacOS
```bash
brew install cmake ninja llvm ccache sdl2 sdl2_image
```

## Usage
### First build
```bash
rm -rf build
cmake -S . -B build -G Ninja -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER_LAUNCHER=ccache -DCMAKE_C_COMPILER_LAUNCHER=ccache
cmake --build build
```

### Compile and run
```bash
alias cr='cmake --build build && ./build/main\

```
Dont forget to make sure ccache is working:
```bash
ccache -s
```
First build -> all misses 
Second build -> should show hits increasing 

### Project structure
MyProject/
 ├─ CMakeLists.txt
 ├─ README.md
 ├─ include/     # headers
 ├─ src/         # sources
 └─ img/         # example assets


