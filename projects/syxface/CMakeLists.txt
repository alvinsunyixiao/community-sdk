cmake_minimum_required(VERSION 3.0.0)
project (syx_face)

set(SYX_FACE_EXE SYXFace)

add_executable(${SYX_FACE_EXE} Socket.cpp FacialExpressionControl.cpp FacialExpressionDemo.cpp)
target_link_libraries(${SYX_FACE_EXE} ${PROJECT_LINK_LIBS})
target_include_directories(${SYX_FACE_EXE}
    PRIVATE
    ${COMMUNITY_SDK_INCLUDE_DIR})
if (WIN32)
    if(MSVC)
        set_target_properties(${SYX_FACE_EXE} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${EXECUTABLE_OUTPUT_PATH}/$<CONFIG>)
    else()
        set_target_properties(${SYX_FACE_EXE} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${EXECUTABLE_OUTPUT_PATH})
    endif()
    add_custom_command(TARGET ${SYX_FACE_EXE} POST_BUILD
              COMMAND ${CMAKE_COMMAND} -E copy_if_different
              ${SDK_DLLS} $<TARGET_FILE_DIR:${SYX_FACE_EXE}>)
endif()

if (APPLE)
    set_target_properties(${SYX_FACE_EXE} PROPERTIES LINK_FLAGS "-F/Library/Frameworks")
endif(APPLE)



