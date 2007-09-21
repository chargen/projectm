PROJECT(projectM-jack)

ADD_EXECUTABLE(projectM-jack projectM-jack.cpp sdltoprojectM.h video_init.cpp ConfigFile.h ConfigFile.cpp)

INCLUDE(FindPkgConfig.cmake)

FIND_PACKAGE(OpenGL)
FIND_PACKAGE(SDL)

pkg_search_module(PROJECTM REQUIRED libprojectM)
pkg_search_module(JACK REQUIRED jack)

ADD_DEFINITIONS(-DLINUX -DPROJECTM_PREFIX='"${PROJECTM_PREFIX}"')

INCLUDE_DIRECTORIES(${PROJECTM_INCLUDEDIR} ${JACK_INCLUDEDIR}  ${SDL_INCLUDE_DIR} ${GTK_INCLUDE_DIR})
LINK_DIRECTORIES(${PROJECTM_LDFLAGS} ${JACK_LDFLAGS})

TARGET_LINK_LIBRARIES(projectM-jack projectM  jack  ${SDL_LIBRARY} ${GTK_LIBRARIES})

INSTALL(TARGETS projectM-jack DESTINATION ${CMAKE_INSTALL_PREFIX}/bin )