cmake_minimum_required(VERSION 3.20)
project(OpenMRac LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# =========================
# Source files
# =========================
file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS
    "*.cpp"
)

# Remove build artifacts if accidentally included
list(FILTER SOURCES EXCLUDE REGEX ".*/build/.*")
list(FILTER SOURCES EXCLUDE REGEX ".*/CMakeFiles/.*")

# =========================
# Executable
# =========================
add_executable(OpenMRac WIN32 ${SOURCES})

# =========================
# Include directories
# =========================
target_include_directories(OpenMRac PRIVATE
    ${CMAKE_SOURCE_DIR}
    C:/msys64/mingw64/include
)

# =========================
# Find core packages
# =========================
find_package(SDL2 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(glm REQUIRED)

# =========================
# IMPORTANT: MSYS2 native libs (NO find_package for jpeg/png/openal)
# =========================

# =========================
# Link libraries
# =========================
target_link_libraries(OpenMRac PRIVATE
    SDL2::SDL2
    OpenGL::GL
    OpenGL::GLU
    GLEW::GLEW

    # MSYS2 / MinGW system libraries
    openal
    jpeg
    png
)

# =========================
# Compile definitions
# =========================
target_compile_definitions(OpenMRac PRIVATE
    SDL_MAIN_HANDLED
    USE_MINIAL
    _USE_MATH_DEFINES
    NDEBUG
)

# =========================
# Windows subsystem (no console)
# =========================
set_target_properties(OpenMRac PROPERTIES
    WIN32_EXECUTABLE TRUE
)