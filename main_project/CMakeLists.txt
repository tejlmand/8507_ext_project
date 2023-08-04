
cmake_minimum_required(VERSION 3.20)

project(main_project LANGUAGES)

include(ExternalProject)

ExternalProject_Add(ext_project
                    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../external_delay_project
                    BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR}/ext
                    BUILD_BYPRODUCTS ${CMAKE_CURRENT_BINARY_DIR}/ext/extproject.txt
                                     ${CMAKE_CURRENT_BINARY_DIR}/ext/extbyproduct.txt
                    INSTALL_COMMAND ""
)

add_custom_target(mainprojtarget ALL
                  ${CMAKE_COMMAND} -E copy ${CMAKE_BINARY_DIR}/ext/extproject.txt ${CMAKE_BINARY_DIR}/copyextproject.txt
                  COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_BINARY_DIR}/ext/extbyproduct.txt ${CMAKE_BINARY_DIR}/copyextbyproduct.txt
                  DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/ext/extproject.txt
                          ${CMAKE_CURRENT_BINARY_DIR}/ext/extbyproduct.txt
                          ext_project
)

