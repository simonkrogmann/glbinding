
# 
# External dependencies
# 

find_package(GLFW)


# 
# Executable name and options
# 

# Target name
set(target glbinding-test)

if (NOT GLFW_FOUND)
    message("Test ${target} skipped: GLFW not found")
    return()
else()
    message(STATUS "Test ${target}")
endif()


# 
# Sources
# 

set(sources
    main.cpp
    AllVersions_test.cpp
    RingBuffer_test.cpp
    SharedBitfield_test.cpp
    
    # regession tests
    Regression_test_82.cpp
)


# 
# Create executable
# 

# Build executable
add_executable(${target}
    ${sources}
)

# Create namespaced alias
add_executable(${META_PROJECT_NAME}::${target} ALIAS ${target})


# 
# Project options
# 

set_target_properties(${target}
    PROPERTIES
    ${DEFAULT_PROJECT_OPTIONS}
    FOLDER "${IDE_FOLDER}"
)


# 
# Include directories
# 

target_include_directories(${target}
    PRIVATE
    ${DEFAULT_INCLUDE_DIRECTORIES}
    ${PROJECT_BINARY_DIR}/source/include
    ${PROJECT_SOURCE_DIR}/source/glbinding/source/
    SYSTEM
    ${GLFW_INCLUDE_DIR}
)


# 
# Libraries
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LIBRARIES}
    ${GLFW_LIBRARY}
    ${META_PROJECT_NAME}::glbinding
    gmock-dev
)


# 
# Compile definitions
# 

target_compile_definitions(${target}
    PRIVATE
    ${DEFAULT_COMPILE_DEFINITIONS}
)


# 
# Compile options
# 

target_compile_options(${target}
    PRIVATE
    ${DEFAULT_COMPILE_OPTIONS}
)


# 
# Linker options
# 

target_link_libraries(${target}
    PRIVATE
    ${DEFAULT_LINKER_OPTIONS}
)
