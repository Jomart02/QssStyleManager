cmake_minimum_required(VERSION 3.5)

set(PROJECT_NAME QssStyleManager)
project(${PROJECT_NAME})

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)


set(HDRS
    ./include/StyleManager.h
)
set(SRC
   ./src/StyleManager.cpp
)



find_package(Qt6 COMPONENTS Widgets REQUIRED)



add_library(${PROJECT_NAME} STATIC ${HDRS} ${SRC})

target_link_libraries(${PROJECT_NAME} Qt6::Widgets )
# Указываем, что заголовочные файлы библиотеки должны быть доступны для других проектов
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
