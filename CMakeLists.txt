cmake_minimum_required(VERSION 3.0.0)
project(UET2022)
include_directories(include)

set(SOURCES source/main.cpp
            source/Render/RenderWindow.cpp
            source/Render/Sprite.cpp
            source/Render/View.cpp
            source/StateMachine.cpp 
            source/Game.cpp
            source/GameState.cpp
            source/AssetManager.cpp
            source/Player.cpp
            source/Map.cpp
            source/Tile.cpp
            source/Animation.cpp
            source/Enemy.cpp
            source/Bullet.cpp
            source/BulletManager.cpp
            source/Render/Text.cpp
            source/MenuState.cpp
            source/WinState.cpp
            source/EnemyManager.cpp
            source/GameOverState.cpp)


find_package(SDL2 REQUIRED)

# if(NOT SDL2_IMAGE_INCLUDE_DIR AND SDL2IMAGE_INCLUDE_DIR)
#   set(SDL2_IMAGE_INCLUDE_DIR ${SDL2IMAGE_INCLUDE_DIR} CACHE PATH "directory cache
# entry initialized from old variable name")
# endif()
find_path(SDL2_IMAGE_INCLUDE_DIR SDL_image.h
  HINTS
    ENV SDL2IMAGEDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES SDL2
                # path suffixes to search inside ENV{SDL2DIR}
                include/SDL2 include
)

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  set(VC_LIB_PATH_SUFFIX lib/x64)
else()
  set(VC_LIB_PATH_SUFFIX lib/x86)
endif()

if(NOT SDL2_IMAGE_LIBRARY AND SDL2IMAGE_LIBRARY)
  set(SDL2_IMAGE_LIBRARY ${SDL2IMAGE_LIBRARY} CACHE FILEPATH "file cache entry
initialized from old variable name")
endif()
find_library(SDL2_IMAGE_LIBRARY
  NAMES SDL2_image
  HINTS
    ENV SDL2IMAGEDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES lib ${VC_LIB_PATH_SUFFIX}
)

if(SDL2_IMAGE_INCLUDE_DIR AND EXISTS "${SDL2_IMAGE_INCLUDE_DIR}/SDL2_image.h")
  file(STRINGS "${SDL2_IMAGE_INCLUDE_DIR}/SDL2_image.h" SDL2_IMAGE_VERSION_MAJOR_LINE REGEX "^#define[ \t]+SDL2_IMAGE_MAJOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_IMAGE_INCLUDE_DIR}/SDL2_image.h" SDL2_IMAGE_VERSION_MINOR_LINE REGEX "^#define[ \t]+SDL2_IMAGE_MINOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_IMAGE_INCLUDE_DIR}/SDL2_image.h" SDL2_IMAGE_VERSION_PATCH_LINE REGEX "^#define[ \t]+SDL2_IMAGE_PATCHLEVEL[ \t]+[0-9]+$")
  string(REGEX REPLACE "^#define[ \t]+SDL2_IMAGE_MAJOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_IMAGE_VERSION_MAJOR "${SDL2_IMAGE_VERSION_MAJOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_IMAGE_MINOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_IMAGE_VERSION_MINOR "${SDL2_IMAGE_VERSION_MINOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_IMAGE_PATCHLEVEL[ \t]+([0-9]+)$" "\\1" SDL2_IMAGE_VERSION_PATCH "${SDL2_IMAGE_VERSION_PATCH_LINE}")
  set(SDL2_IMAGE_VERSION_STRING ${SDL2_IMAGE_VERSION_MAJOR}.${SDL2_IMAGE_VERSION_MINOR}.${SDL2_IMAGE_VERSION_PATCH})
  unset(SDL2_IMAGE_VERSION_MAJOR_LINE)
  unset(SDL2_IMAGE_VERSION_MINOR_LINE)
  unset(SDL2_IMAGE_VERSION_PATCH_LINE)
  unset(SDL2_IMAGE_VERSION_MAJOR)
  unset(SDL2_IMAGE_VERSION_MINOR)
  unset(SDL2_IMAGE_VERSION_PATCH)
endif()

set(SDL2_IMAGE_LIBRARIES ${SDL2_IMAGE_LIBRARY})
set(SDL2_IMAGE_INCLUDE_DIRS ${SDL2_IMAGE_INCLUDE_DIR})

include(FindPackageHandleStandardArgs)

FIND_PACKAGE_HANDLE_STANDARD_ARGS(SDL2_image
                                  REQUIRED_VARS SDL2_IMAGE_LIBRARIES SDL2_IMAGE_INCLUDE_DIRS
                                  VERSION_VAR SDL2_IMAGE_VERSION_STRING)

# for backward compatibility
set(SDL2IMAGE_LIBRARY ${SDL2_IMAGE_LIBRARIES})
set(SDL2IMAGE_INCLUDE_DIR ${SDL2_IMAGE_INCLUDE_DIRS})
set(SDL2IMAGE_FOUND ${SDL2_IMAGE_FOUND})



INCLUDE_DIRECTORIES(${SDL2_INCLUDE_DIRS} ${SDL2IMAGE_INCLUDE_DIR})



#****************************************************
find_path(SDL2_TTF_INCLUDE_DIR SDL_ttf.h
  HINTS
    ENV SDL2TTFDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES SDL2
                # path suffixes to search inside ENV{SDL2DIR}
                include/SDL2 include
)
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  set(VC_LIB_PATH_SUFFIX lib/x64)
else()
  set(VC_LIB_PATH_SUFFIX lib/x86)
endif()
if(NOT SDL2_TTF_LIBRARY AND SDL2TTF_LIBRARY)
  set(SDL2_TTF_LIBRARY ${SDL2TTF_LIBRARY} CACHE FILEPATH "file cache entry
initialized from old variable name")
endif()
find_library(SDL2_TTF_LIBRARY
  NAMES SDL2_ttf
  HINTS
    ENV SDL2TTFDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES lib ${VC_LIB_PATH_SUFFIX}
)
if(SDL2_TTF_INCLUDE_DIR AND EXISTS "${SDL2_TTF_INCLUDE_DIR}/SDL2_ttf.h")
  file(STRINGS "${SDL2_TTF_INCLUDE_DIR}/SDL2_ttf.h" SDL2_TTF_VERSION_MAJOR_LINE REGEX "^#define[ \t]+SDL2_TTF_MAJOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_TTF_INCLUDE_DIR}/SDL2_ttf.h" SDL2_TTF_VERSION_MINOR_LINE REGEX "^#define[ \t]+SDL2_TTF_MINOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_TTF_INCLUDE_DIR}/SDL2_ttf.h" SDL2_TTF_VERSION_PATCH_LINE REGEX "^#define[ \t]+SDL2_TTF_PATCHLEVEL[ \t]+[0-9]+$")
  string(REGEX REPLACE "^#define[ \t]+SDL2_TTF_MAJOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_TTF_VERSION_MAJOR "${SDL2_TTF_VERSION_MAJOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_TTF_MINOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_TTF_VERSION_MINOR "${SDL2_TTF_VERSION_MINOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_TTF_PATCHLEVEL[ \t]+([0-9]+)$" "\\1" SDL2_TTF_VERSION_PATCH "${SDL2_TTF_VERSION_PATCH_LINE}")
  set(SDL2_TTF_VERSION_STRING ${SDL2_TTF_VERSION_MAJOR}.${SDL2_TTF_VERSION_MINOR}.${SDL2_TTF_VERSION_PATCH})
  unset(SDL2_TTF_VERSION_MAJOR_LINE)
  unset(SDL2_TTF_VERSION_MINOR_LINE)
  unset(SDL2_TTF_VERSION_PATCH_LINE)
  unset(SDL2_TTF_VERSION_MAJOR)
  unset(SDL2_TTF_VERSION_MINOR)
  unset(SDL2_TTF_VERSION_PATCH)
endif()

set(SDL2_TTF_LIBRARIES ${SDL2_TTF_LIBRARY})
set(SDL2_TTF_INCLUDE_DIRS ${SDL2_TTF_INCLUDE_DIR})

FIND_PACKAGE_HANDLE_STANDARD_ARGS(SDL2_ttf
                                  REQUIRED_VARS SDL2_TTF_LIBRARIES SDL2_TTF_INCLUDE_DIRS
                                  VERSION_VAR SDL2_TTF_VERSION_STRING)

# for backward compatibility
set(SDL2TTF_LIBRARY ${SDL2_TTF_LIBRARIES})
set(SDL2TTF_INCLUDE_DIR ${SDL2_TTF_INCLUDE_DIRS})
set(SDL2TTF_FOUND ${SDL2_TTF_FOUND})


INCLUDE_DIRECTORIES(${SDL2_INCLUDE_DIRS} ${SDL2TTF_INCLUDE_DIR})
#***************************************************



#***************************************************
find_path(SDL2_MIXER_INCLUDE_DIR SDL_mixer.h
  HINTS
    ENV SDL2MIXERDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES SDL2
                # path suffixes to search inside ENV{SDL2DIR}
                include/SDL2 include
)
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  set(VC_LIB_PATH_SUFFIX lib/x64)
else()
  set(VC_LIB_PATH_SUFFIX lib/x86)
endif()
if(NOT SDL2_MIXER_LIBRARY AND SDL2MIXER_LIBRARY)
  set(SDL2_MIXER_LIBRARY ${SDL2MIXER_LIBRARY} CACHE FILEPATH "file cache entry
initialized from old variable name")
endif()
find_library(SDL2_MIXER_LIBRARY
  NAMES SDL2_mixer
  HINTS
    ENV SDL2MIXERDIR
    ENV SDL2DIR
    ${SDL2_DIR}
  PATH_SUFFIXES lib ${VC_LIB_PATH_SUFFIX}
)
if(SDL2_MIXER_INCLUDE_DIR AND EXISTS "${SDL2_MIXER_INCLUDE_DIR}/SDL2_mixer.h")
  file(STRINGS "${SDL2_MIXER_INCLUDE_DIR}/SDL2_mixer.h" SDL2_MIXER_VERSION_MAJOR_LINE REGEX "^#define[ \t]+SDL2_MIXER_MAJOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_MIXER_INCLUDE_DIR}/SDL2_mixer.h" SDL2_MIXER_VERSION_MINOR_LINE REGEX "^#define[ \t]+SDL2_MIXER_MINOR_VERSION[ \t]+[0-9]+$")
  file(STRINGS "${SDL2_MIXER_INCLUDE_DIR}/SDL2_mixer.h" SDL2_MIXER_VERSION_PATCH_LINE REGEX "^#define[ \t]+SDL2_MIXER_PATCHLEVEL[ \t]+[0-9]+$")
  string(REGEX REPLACE "^#define[ \t]+SDL2_MIXER_MAJOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_MIXER_VERSION_MAJOR "${SDL2_MIXER_VERSION_MAJOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_MIXER_MINOR_VERSION[ \t]+([0-9]+)$" "\\1" SDL2_MIXER_VERSION_MINOR "${SDL2_MIXER_VERSION_MINOR_LINE}")
  string(REGEX REPLACE "^#define[ \t]+SDL2_MIXER_PATCHLEVEL[ \t]+([0-9]+)$" "\\1" SDL2_MIXER_VERSION_PATCH "${SDL2_MIXER_VERSION_PATCH_LINE}")
  set(SDL2_MIXER_VERSION_STRING ${SDL2_MIXER_VERSION_MAJOR}.${SDL2_MIXER_VERSION_MINOR}.${SDL2_MIXER_VERSION_PATCH})
  unset(SDL2_MIXER_VERSION_MAJOR_LINE)
  unset(SDL2_MIXER_VERSION_MINOR_LINE)
  unset(SDL2_MIXER_VERSION_PATCH_LINE)
  unset(SDL2_MIXER_VERSION_MAJOR)
  unset(SDL2_MIXER_VERSION_MINOR)
  unset(SDL2_MIXER_VERSION_PATCH)
endif()

set(SDL2_MIXER_LIBRARIES ${SDL2_MIXER_LIBRARY})
set(SDL2_MIXER_INCLUDE_DIRS ${SDL2_MIXER_INCLUDE_DIR})

FIND_PACKAGE_HANDLE_STANDARD_ARGS(SDL2_mixer
                                  REQUIRED_VARS SDL2_MIXER_LIBRARIES SDL2_MIXER_INCLUDE_DIRS
                                  VERSION_VAR SDL2_MIXER_VERSION_STRING)

# for backward compatibility
set(SDL2MIXER_LIBRARY ${SDL2_MIXER_LIBRARIES})
set(SDL2MIXER_INCLUDE_DIR ${SDL2_MIXER_INCLUDE_DIRS})
set(SDL2MIXER_FOUND ${SDL2_MIXER_FOUND})


INCLUDE_DIRECTORIES(${SDL2_INCLUDE_DIRS} ${SDL2MIXER_INCLUDE_DIR})
#***************************************************




#file(GLOB SOURCES "source/*.cpp")

add_executable(main ${SOURCES})
target_link_libraries(main ${SDL2_LIBRARIES} ${SDL2IMAGE_LIBRARY} ${SDL2TTF_LIBRARY} ${SDL2MIXER_LIBRARY})