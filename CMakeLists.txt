cmake_minimum_required(VERSION 3.10)

project(NVClusterSupport)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

set(NVAPI_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/nvapi" CACHE STRING "Path to NVAPI include headers/shaders" )
set(NVAPI_LIBRARY "${CMAKE_SOURCE_DIR}/nvapi/amd64/nvapi64.lib" CACHE STRING "Path to NVAPI .lib file")

if (MSVC)
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /D_ITERATOR_DEBUG_LEVEL=1")
endif()

include_directories(${NVAPI_INCLUDE_DIR})

option(BUILD_DISPLAY_CONF "Build Display Configuration Example" ON)
option(BUILD_QSYNC_EVENT_REG "Build QSYNC Event Registration Example" OFF)
option(BUILD_SYNC_CONF "Build Sync Configuration Example" ON)

# Build Display Configuration Registration
if(BUILD_DISPLAY_CONF)
	set(DISPLAYCONF ${NVAPI_INCLUDE_DIR}/Sample_Code/DisplayConfiguration/DisplayConfiguration.cpp)
	add_executable(Display_Configuration ${DISPLAYCONF})
	target_link_libraries(Display_Configuration ${NVAPI_LIBRARY})
endif()

# Build QSYNC Event Registration
if(BUILD_QSYNC_EVENT_REG)
	set(SYNCEVENTREG ${NVAPI_INCLUDE_DIR}/Sample_Code/QSYNC_Event_Registration/QSYNC_Event_Registration.cpp)
	add_executable(QSYNC_Event_Registration ${SYNCEVENTREG})
	target_link_libraries(QSYNC_Event_Registration ${NVAPI_LIBRARY})
endif()

# Build Sync Configuration Example
if(BUILD_SYNC_CONF)
	set(SYNCCONF ${NVAPI_INCLUDE_DIR}/Sample_Code/Sync_Configuration/Sync_Configuration.cpp)
	add_executable(Sync_Configuration ${SYNCCONF})
	target_link_libraries(Sync_Configuration ${NVAPI_LIBRARY})
endif()


