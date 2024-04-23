cmake_minimum_required(VERSION 3.10)

project(MyQtApp)

# Найдем пакет Qt5
find_package(Qt5 COMPONENTS Widgets REQUIRED)

# Добавим исполняемый файл
add_executable(MyQtApp main.cpp)

# Свяжем библиотеки Qt с нашим приложением
target_link_libraries(MyQtApp Qt5::Widgets)
find_package(Doxygen)
if(DOXYGEN_FOUND)
    set(DOXYGEN_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/EduCadDocumentation")
    add_custom_target(doc
        COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile
        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        COMMENT "Generating Doxygen documentation"
        VERBATIM
    )
else()
    add_custom_target(doc
        COMMAND ${CMAKE_COMMAND} -E echo "Doxygen not found. Documentation will not be generated."
        COMMENT "Doxygen not found, skipping documentation generation."
        VERBATIM
    )
endif()
