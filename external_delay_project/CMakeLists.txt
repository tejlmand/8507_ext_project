
cmake_minimum_required(VERSION 3.20)

project(ext_project LANGUAGES)

add_custom_target(maintarget ALL
                  ${CMAKE_COMMAND} -E touch ${CMAKE_BINARY_DIR}/extproject.txt
                  BYPRODUCTS ${CMAKE_BINARY_DIR}/extproject.txt
)


add_custom_command(TARGET maintarget
                   POST_BUILD
                   maintarget 
                   COMMAND ${CMAKE_COMMAND} -E sleep 5 
                   COMMAND ${CMAKE_COMMAND} -E touch ${CMAKE_BINARY_DIR}/extbyproduct.txt
                   BYPRODUCTS ${CMAKE_BINARY_DIR}/extbyproduct.txt
)

