cmake_minimum_required(VERSION 3.14)

set(VER_MAJ 1)
set(VER_MIN 0)
set(VER_PAT 2)
if(NOT DEFINED VER_REL)
    set(VER_REL 1)
endif()
# set(REL_STATUS "rc5")

# QSettings uses these names to derive the per-user settings path.
set(APP_NAME "KLens")
set(APP_DISPLAY_NAME "KLens")
set(ORG_NAME "KLens")
set(ORG_DOMAIN "")

set(VERSION "${VER_MAJ}.${VER_MIN}.${VER_PAT}")

project(klens VERSION ${VERSION} HOMEPAGE_URL "https://github.com/nevaranvik-lang/KLens" LANGUAGES C CXX)

if(NOT CMAKE_SYSTEM_NAME STREQUAL "Linux" OR NOT EXISTS "/etc/os-release")
    message(FATAL_ERROR "KLens supports Debian and Ubuntu Linux only.")
endif()
file(STRINGS "/etc/os-release" KLENS_OS_ID_LINE REGEX "^ID=")
if(NOT KLENS_OS_ID_LINE MATCHES "^ID=(debian|ubuntu)$")
    message(FATAL_ERROR "KLens supports Debian and Ubuntu Linux only.")
endif()

include(GNUInstallDirs)

if(WIN32)
    add_compile_definitions(NOMINMAX WIN32_LEAN_AND_MEAN)
    add_compile_options(
        $<$<COMPILE_LANGUAGE:C,CXX>:/FIwindows.h>
        $<$<COMPILE_LANGUAGE:C,CXX>:/Zc:__cplusplus>
    )
endif()

if(DEFINED VER_REL AND ${VER_REL} GREATER 0)
    set(VERSION "${VERSION}-${VER_REL}")
endif()

if(DEFINED REL_STATUS)
    set(VERSION "${VERSION}-${REL_STATUS}")
endif()

### Packager and Git commit
execute_process(COMMAND git -C ${CMAKE_SOURCE_DIR} log --pretty=format:%h -n 1
    OUTPUT_VARIABLE GIT_COMMIT
    ERROR_QUIET
)

if (EXISTS "${CMAKE_SOURCE_DIR}/debian/git-build-recipe.manifest")
    set(PACKAGER "PPA")

    if ("${GIT_COMMIT}" STREQUAL "")
        file(READ "${CMAKE_SOURCE_DIR}/debian/git-build-recipe.manifest" PPA_MANIFEST)
        string(REGEX MATCH "lp:cctv-viewer git-commit:(.......)" _ ${PPA_MANIFEST})
        set(GIT_COMMIT ${CMAKE_MATCH_1})
    endif()
endif()

if(NOT DEFINED PACKAGER)
    if ("${GIT_COMMIT}" STREQUAL "")
        set(PACKAGER "SRC")
    else()
        set(PACKAGER "GIT")
    endif()
endif()

if ("${GIT_COMMIT}" STREQUAL "")
    set(GIT_COMMIT "N/A")
endif()

set(VERSION "${VERSION} ${PACKAGER}.${GIT_COMMIT} (${CMAKE_SYSTEM_PROCESSOR})")
###

add_compile_definitions(
    $<$<COMPILE_LANGUAGE:C,CXX>:APP_NAME="${APP_NAME}">
    $<$<COMPILE_LANGUAGE:C,CXX>:APP_DISPLAY_NAME="${APP_DISPLAY_NAME}">
    $<$<COMPILE_LANGUAGE:C,CXX>:APP_VERSION="${VERSION}">
    $<$<COMPILE_LANGUAGE:C,CXX>:ORG_NAME="${ORG_NAME}">
    $<$<COMPILE_LANGUAGE:C,CXX>:ORG_DOMAIN="${ORG_DOMAIN}">
)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Fix build on LP for Ubuntu 20.04
if(NOT WIN32)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Debug" AND NOT ANDROID)
    add_compile_options(
        -Werror
        -pedantic-errors

        -Wall
        -Wextra
        -Wpedantic

        -Wcast-align
        -Wcast-qual
        # -Wconversion
        -Wctor-dtor-privacy
        -Wduplicated-branches
        -Wduplicated-cond
        -Wextra-semi
        -Wfloat-equal
        -Wlogical-op
        -Wnon-virtual-dtor
        -Wold-style-cast
        # -Woverloaded-virtual
        -Wredundant-decls
        # -Wsign-conversion
        # -Wsign-promo
    )
endif()

# Disable use of C++ API deprecated in Qt 5.15
add_compile_definitions(QT_DISABLE_DEPRECATED_BEFORE=0x050F00)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check https://doc.qt.io/qt/deployment-android.html for more information.
# They need to be set before the find_package(...) calls below.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

set(QT_LINK_DEPENDENCIES Core Quick Multimedia Network Widgets)

if (ANDROID)
    list(APPEND QT_LINK_DEPENDENCIES Svg)

    set(ANDROID_EXTRA_LIBS
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libavformat.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libavcodec.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libavutil.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libswscale.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libswresample.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libavdevice.so"
        "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib/libavfilter.so"
        )
else()
    if(WIN32)
        include_directories(${FFMPEG_INC})
        link_directories(${FFMPEG_LIB})
    else()
        find_package(PkgConfig REQUIRED)
        pkg_check_modules(LIBAV REQUIRED
            libavformat
            libavcodec
            libavutil
            libswscale
            libswresample
            libavdevice
        )
        include_directories(${LIBAV_INCLUDE_DIRS})
    endif()
endif()

find_package(QT NAMES Qt5 COMPONENTS ${QT_LINK_DEPENDENCIES} QuickCompiler LinguistTools REQUIRED)
find_package(Qt5 5.12 COMPONENTS ${QT_LINK_DEPENDENCIES} QuickCompiler LinguistTools REQUIRED)

file(GLOB TS_FILES "${CMAKE_SOURCE_DIR}/translations/*.ts")

set_source_files_properties(${TS_FILES} PROPERTIES OUTPUT_LOCATION "${CMAKE_SOURCE_DIR}/translations")
if (${QT_VERSION_MAJOR} GREATER 5)
    qt_add_translation(QM_FILES ${TS_FILES})
else()
    qt5_add_translation(QM_FILES ${TS_FILES})
endif()


if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    if (${QT_VERSION_MAJOR} GREATER 5)
        qt_add_resources(RESOURCES klens.qrc)
    else()
        qt5_add_resources(RESOURCES klens.qrc)
    endif()
else()
    qtquick_compiler_add_resources(RESOURCES klens.qrc)
endif()

set(PROJ_FILES
    src/main.cpp
    src/clipboard.h
    src/singleapplication.h
    src/config.cpp src/config.h
    src/context.cpp src/context.h
    src/eventfilter.h src/eventfilter.cpp
    src/viewportslayoutmodel.cpp src/viewportslayoutmodel.h
    src/viewportslayoutscollectionmodel.cpp src/viewportslayoutscollectionmodel.h
    src/hikvisionmanager.cpp src/hikvisionmanager.h
    src/hikvisionplayer.cpp src/hikvisionplayer.h
    src/thumbnailprovider.cpp src/thumbnailprovider.h
    src/hikvisionisapi.cpp src/hikvisionisapi.h
    src/hikvisionarchiveplayer.cpp src/hikvisionarchiveplayer.h
    src/hikvisiondownloader.cpp src/hikvisiondownloader.h
    src/systemstats.cpp src/systemstats.h
    src/nvrstatusmanager.cpp src/nvrstatusmanager.h
    src/DownloadDialog.qml
    src/NvrStatusDialog.qml
    ${RESOURCES}
    ${TS_FILES}
    ${QM_FILES}
    )

set(QML_IMPORT_PATH "${CMAKE_SOURCE_DIR}/src/imports" CACHE STRING "Additional import path used to resolve QML modules in Qt Creator's code model")

add_subdirectory(src/qmlav)

if (ANDROID)
    add_library(klens SHARED ${PROJ_FILES} ${QMLAV_FILES})

    target_include_directories(klens PRIVATE "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/include")
    target_link_directories(klens PRIVATE "${CMAKE_SOURCE_DIR}/src/qmlav/3rd/FFmpeg/ffbuild/${ANDROID_ABI}/lib")
else()
    if(WIN32)
        list(APPEND PROJ_FILES klens.rc)
    endif()
    add_executable(klens ${PROJ_FILES} ${QMLAV_FILES})
    if(WIN32)
        set_target_properties(klens PROPERTIES WIN32_EXECUTABLE TRUE)
    endif()
endif()

target_include_directories(klens PRIVATE ${QMLAV_INCLUDE})

target_compile_definitions(klens
    PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)

foreach (ITEM ${QT_LINK_DEPENDENCIES})
    target_link_libraries(klens PRIVATE Qt${QT_VERSION_MAJOR}::${ITEM})
endforeach()
target_link_libraries(klens PRIVATE ${QMLAV_LINK_DEPENDENCIES})
target_include_directories(klens PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/inc")
target_link_directories(klens PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib")
target_link_libraries(klens PRIVATE hcnetsdk PlayCtrl)
# Use RPATH (not RUNPATH) so transitive deps (libAudioRender.so, libSuperRender.so) loaded
# by libPlayCtrl.so/libhcnetsdk.so can also be found via this path.
if(UNIX)
target_link_options(klens PRIVATE
    "LINKER:--disable-new-dtags"
    "LINKER:-rpath-link,${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib"
)
endif()
set_target_properties(klens PROPERTIES
    BUILD_RPATH "\$ORIGIN/../src/hikvision_sdk/lib"
    INSTALL_RPATH "\$ORIGIN/../${CMAKE_INSTALL_LIBDIR}/klens"
    BUILD_WITH_INSTALL_RPATH FALSE
    INSTALL_RPATH_USE_LINK_PATH FALSE
)
if (NOT ANDROID)
    set_target_properties(klens PROPERTIES OUTPUT_NAME "klens")

    add_executable(diagnose_archive src/diagnose_archive.cpp)
    target_include_directories(diagnose_archive PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/inc")
    target_link_directories(diagnose_archive PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib")
    target_link_libraries(diagnose_archive PRIVATE hcnetsdk PlayCtrl Qt5::Widgets)
    if(UNIX)
    target_link_options(diagnose_archive PRIVATE 
        "LINKER:--disable-new-dtags"
        "LINKER:-rpath-link,${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib"
    )
    endif()
    set_target_properties(diagnose_archive PROPERTIES
        BUILD_RPATH "\$ORIGIN/../src/hikvision_sdk/lib"
    )

    add_executable(diagnose_live src/diagnose_live.cpp)
    target_include_directories(diagnose_live PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/inc")
    target_link_directories(diagnose_live PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib")
    target_link_libraries(diagnose_live PRIVATE hcnetsdk PlayCtrl Qt5::Widgets)
    if(UNIX)
    target_link_options(diagnose_live PRIVATE 
        "LINKER:--disable-new-dtags"
        "LINKER:-rpath-link,${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib"
    )
    endif()
    set_target_properties(diagnose_live PROPERTIES
        BUILD_RPATH "\$ORIGIN/../src/hikvision_sdk/lib"
    )

    add_executable(diagnose_compression src/diagnose_compression.cpp)
    target_include_directories(diagnose_compression PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/inc")
    target_link_directories(diagnose_compression PRIVATE "${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib")
    target_link_libraries(diagnose_compression PRIVATE hcnetsdk PlayCtrl Qt5::Widgets)
    if(UNIX)
    target_link_options(diagnose_compression PRIVATE 
        "LINKER:--disable-new-dtags"
        "LINKER:-rpath-link,${CMAKE_SOURCE_DIR}/src/hikvision_sdk/lib"
    )
    endif()
    set_target_properties(diagnose_compression PROPERTIES
        BUILD_RPATH "\$ORIGIN/../src/hikvision_sdk/lib"
    )
endif()

set_directory_properties(PROPERTIES CLEAN_NO_CUSTOM true)

if (UNIX AND NOT ANDROID)
    set(CMAKE_INSTALL_PREFIX "/usr")
    install(TARGETS klens DESTINATION "${CMAKE_INSTALL_BINDIR}")
    install(FILES "images/128.png" DESTINATION "/usr/share/icons/hicolor/128x128/apps" RENAME "klens.png")
    install(FILES "images/256.png" DESTINATION "/usr/share/icons/hicolor/256x256/apps" RENAME "klens.png")
    install(FILES "images/512.png" DESTINATION "/usr/share/icons/hicolor/512x512/apps" RENAME "klens.png")
    install(FILES "images/512.png" DESTINATION "/usr/share/pixmaps" RENAME "klens.png")
    install(FILES "klens.desktop" DESTINATION "/usr/share/applications")
    install(DIRECTORY "src/hikvision_sdk/lib/" DESTINATION "${CMAKE_INSTALL_LIBDIR}/klens")
endif()
