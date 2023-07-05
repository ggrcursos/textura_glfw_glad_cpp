file(GLOB_RECURSE texture2D_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp") 
file(GLOB_RECURSE texture2D_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp") 

 
set (texture2D_INCLUDE_DIRS "")
foreach (_headerFile ${texture2D_HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND texture2D_INCLUDE_DIRS ${_dir})
endforeach()
 
list(REMOVE_DUPLICATES texture2D_INCLUDE_DIRS)
add_executable(texture2DExec ${texture2D_SOURCES} ${texture2D_HEADERS}  ${OPENGL_LIBRARIES}    )
add_library(texture2D ${texture2D_SOURCES} ${texture2D_HEADERS}  ${OPENGL_LIBRARIES}    )
target_include_directories(texture2D PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/")
set_target_properties(texture2D PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${INSTALLATION_PATH}/)
install(TARGETS texture2D DESTINATION ${INSTALLATION_PATH}/)

set(texture2D_TARGET_LIBRARIES
    ${CMAKE_THREAD_LIBS_INIT} #pthread 
    glad
    glfw
    )
  
target_link_libraries(texture2D ${texture2D_TARGET_LIBRARIES}   ${OPENGL_LIBRARIES})
target_link_libraries(texture2DExec ${texture2D_TARGET_LIBRARIES}   ${OPENGL_LIBRARIES})
