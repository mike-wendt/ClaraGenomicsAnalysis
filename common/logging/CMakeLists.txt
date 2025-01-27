#
# Copyright (c) 2019, NVIDIA CORPORATION.  All rights reserved.
#
# NVIDIA CORPORATION and its licensors retain all intellectual property
# and proprietary rights in and to this software, related documentation
# and any modifications thereto.  Any use, reproduction, disclosure or
# distribution of this software and related documentation without an express
# license agreement from NVIDIA CORPORATION is strictly prohibited.
#

project(logging)

add_library(logging
        src/logging.cpp)
target_link_libraries(logging PUBLIC spdlog pthread)

add_doxygen_source_dir(${CMAKE_CURRENT_SOURCE_DIR}/include/logging)

target_include_directories(logging
    PUBLIC 
        $<INSTALL_INTERFACE:include>    
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_compile_options(logging PRIVATE -Werror)

install(TARGETS logging 
    EXPORT logging
    DESTINATION lib
    INCLUDES DESTINATION include
)
install(DIRECTORY include/ DESTINATION include)
install(EXPORT logging DESTINATION cmake)

# Add auto formatting.
cga_enable_auto_formatting("${CMAKE_CURRENT_SOURCE_DIR}")
