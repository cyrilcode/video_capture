
include_directories(include)
set(SOURCE_FILES
        src/videocapture/Base.cpp
        src/videocapture/CapabilityFinder.cpp
        src/videocapture/Capture.cpp
        src/videocapture/Types.cpp
        src/videocapture/Utils.cpp
        )

add_library(vidcap ${SOURCE_FILES})

#TODO: only do this on mac
set(VIDCAP_MAC_FILES
        src/videocapture/mac/AVFoundation_Capture.cpp
        src/videocapture/mac/AVFoundation_Implementation.mm)
find_library(CORE_FOUNDATION CoreFoundation)
find_library(AV_FOUNDATION AvFoundation)
find_library(COCOA Cocoa)
find_library(CORE_VIDEO CoreVideo)
find_library(CORE_MEDIA CoreMedia)
add_library(vidcap_mac ${VIDCAP_MAC_FILES})
target_link_libraries(vidcap vidcap_mac ${CORE_FOUNDATION} ${AV_FOUNDATION}
        ${COCOA} ${CORE_VIDEO} ${CORE_MEDIA})
#end of mac stuff

set(VIDCAP_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include PARENT_SCOPE)
set(VIDCAP_LIBRARIES vidcap PARENT_SCOPE)
