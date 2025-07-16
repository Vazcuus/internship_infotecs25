cmake_minimum_required(VERSION 3.10)
project(SQLite VERSION 1.0)

# Стандарт плюсов устанавливаем
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Сурсы
set(SOURCES
    src/sqlite3.c
    src/sqlite3.h
)

# Create shared library target
add_library(${PROJECT_NAME} SHARED ${SOURCES})

# Настройки винды
if(WIN32)
    # флажки
    if(MSVC)
        target_compile_options(${PROJECT_NAME} PRIVATE /W4)
        target_compile_definitions(${PROJECT_NAME} PRIVATE "BUILDING_DLL")
    endif()
    
    # имя длл для разных архитектур
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}_x64")
    else()
        set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}_x86")
    endif()
endif()

# линукс настройки
if(UNIX AND NOT APPLE)

    set(CMAKE_C_COMPILER "gcc")
    set(CMAKE_CXX_COMPILER "g++")

    # флажки гцц
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra)

    # имя длл для разных архитектур
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}_x64")
    else()
        set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}_x86")
    endif()
endif()


if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_VERBOSE_MAKEFILE ON)
endif()

# выходные директории
set_target_properties(${PROJECT_NAME} PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
)