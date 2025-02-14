cmake_minimum_required(VERSION 3.15)
project(Cardinal VERSION 23.07)

include(FetchContent)
FetchContent_Declare(JUCE
  GIT_REPOSITORY https://github.com/DISTRHO/JUCE.git
  GIT_TAG v6.1.6
  GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(JUCE)

# Config

set(CMAKE_C_VISIBILITY_PRESET hidden)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)

# Define static libs

add_library(dgl STATIC IMPORTED)
set_property(TARGET dgl PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../dpf/build/libdgl-opengl.a")

add_library(carla_host_plugin STATIC IMPORTED)
set_property(TARGET carla_host_plugin PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/plugin/${CMAKE_BUILD_TYPE}/carla-host-plugin.cpp.o")

add_library(carla_engine_plugin STATIC IMPORTED)
set_property(TARGET carla_engine_plugin PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/carla_engine_plugin.a")

add_library(carla_plugin STATIC IMPORTED)
set_property(TARGET carla_plugin PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/carla_plugin.a")

add_library(native_plugins STATIC IMPORTED)
set_property(TARGET native_plugins PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/native-plugins.a")

add_library(audio_decoder STATIC IMPORTED)
set_property(TARGET audio_decoder PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/audio_decoder.a")

add_library(jackbridge STATIC IMPORTED)
set_property(TARGET jackbridge PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/jackbridge.min.a")

add_library(lilv STATIC IMPORTED)
set_property(TARGET lilv PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/lilv.a")

add_library(rtmempool STATIC IMPORTED)
set_property(TARGET rtmempool PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/rtmempool.a")

add_library(water STATIC IMPORTED)
set_property(TARGET water PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/water.a")

add_library(ysfx STATIC IMPORTED)
set_property(TARGET ysfx PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/ysfx.a")

add_library(zita_resampler STATIC IMPORTED)
set_property(TARGET zita_resampler PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../carla/build/modules/${CMAKE_BUILD_TYPE}/zita-resampler.a")

add_library(sCardinal STATIC IMPORTED)
set_property(TARGET sCardinal PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../bin/Cardinal.a")

add_library(sCardinalFX STATIC IMPORTED)
set_property(TARGET sCardinalFX PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../bin/CardinalFX.a")

add_library(sCardinalSynth STATIC IMPORTED)
set_property(TARGET sCardinalSynth PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../bin/CardinalSynth.a")

add_library(sPlugins STATIC IMPORTED)
set_property(TARGET sPlugins PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../plugins/plugins.a")

add_library(sRack STATIC IMPORTED)
set_property(TARGET sRack PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/rack.a")

add_library(libaubio STATIC IMPORTED)
set_property(TARGET libaubio PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../deps/aubio/libaubio.a")

add_library(libarchive STATIC IMPORTED)
if (WIN32)
set_property(TARGET libarchive PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libarchive_static.a")
else (WIN32)
set_property(TARGET libarchive PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libarchive.a")
endif (WIN32)

add_library(libjansson STATIC IMPORTED)
set_property(TARGET libjansson PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libjansson.a")

add_library(libquickjs STATIC IMPORTED)
set_property(TARGET libquickjs PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libquickjs.a")

add_library(libsamplerate STATIC IMPORTED)
set_property(TARGET libsamplerate PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libsamplerate.a")

add_library(libspeexdsp STATIC IMPORTED)
set_property(TARGET libspeexdsp PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libspeexdsp.a")

add_library(libzstd STATIC IMPORTED)
set_property(TARGET libzstd PROPERTY IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/../src/Rack/dep/lib/libzstd.a")

set(SURGE_DEP_PATH "${PROJECT_SOURCE_DIR}/../deps/surge-build")

add_library(surgedep01 STATIC IMPORTED)
add_library(surgedep02 STATIC IMPORTED)
add_library(surgedep03 STATIC IMPORTED)
add_library(surgedep04 STATIC IMPORTED)
add_library(surgedep05 STATIC IMPORTED)
add_library(surgedep06 STATIC IMPORTED)
add_library(surgedep07 STATIC IMPORTED)
#add_library(surgedep08 STATIC IMPORTED)
add_library(surgedep09 STATIC IMPORTED)
add_library(surgedep10 STATIC IMPORTED)

set_property(TARGET surgedep01 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/src/common/libsurge-common.a")
set_property(TARGET surgedep02 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/src/common/libjuce_dsp_rack_sub.a")
set_property(TARGET surgedep03 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/airwindows/libairwindows.a")
set_property(TARGET surgedep04 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/eurorack/libeurorack.a")
set_property(TARGET surgedep05 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/fmt/libfmt.a")
set_property(TARGET surgedep06 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/sqlite-3.23.3/libsqlite.a")
set_property(TARGET surgedep07 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/sst/sst-plugininfra/libsst-plugininfra.a")
#set_property(TARGET surgedep08 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/sst/sst-plugininfra/libs/filesystem/libfilesystem.a")
set_property(TARGET surgedep09 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/sst/sst-plugininfra/libs/strnatcmp/libstrnatcmp.a")
set_property(TARGET surgedep10 PROPERTY IMPORTED_LOCATION "${SURGE_DEP_PATH}/libs/sst/sst-plugininfra/libs/tinyxml/libtinyxml.a")

# dependencies

find_package(PkgConfig REQUIRED)
pkg_check_modules(FFTW3F REQUIRED fftw3f)
pkg_check_modules(LIBLO REQUIRED liblo)
pkg_check_modules(SNDFILE REQUIRED sndfile)

if (APPLE)
set(EXTRA_LIBS "-lz")
set(GL_LIBRARIES "-framework OpenGL")
set(PLUGIN_FORMATS AU)
else (APPLE)
pkg_check_modules(DBUS REQUIRED dbus-1)
pkg_check_modules(GL REQUIRED gl)
pkg_check_modules(X11 REQUIRED x11)
pkg_check_modules(XCURSOR REQUIRED xcursor)
pkg_check_modules(XEXT REQUIRED xext)
pkg_check_modules(XRANDR REQUIRED xrandr)
set(EXTRA_LIBS "-lrt")
set(STATIC_LIBS_START "-Wl,--whole-archive")
set(STATIC_LIBS_END "-Wl,--no-whole-archive")
set(PLUGIN_FORMATS Standalone VST3)
endif (APPLE)

# Main variant

#[[
juce_add_plugin(Cardinal
    AU_MAIN_TYPE kAudioUnitType_MusicEffect
    COMPANY_COPYRIGHT "GPL-3.0-or-later"
    COMPANY_NAME "DISTRHO"
    COMPANY_WEBSITE "https://github.com/DISTRHO/Cardinal"
    DESCRIPTION "Virtual modular synthesizer plugin"
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    FORMATS ${PLUGIN_FORMATS}
    IS_MIDI_EFFECT FALSE
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT TRUE
    NEEDS_MIDI_OUTPUT TRUE
    PLUGIN_CODE DcnM
    PLUGIN_MANUFACTURER_CODE Dstr
    PRODUCT_NAME "Cardinal")

target_sources(Cardinal
    PRIVATE
        CardinalWrapper.cpp)

target_include_directories(Cardinal
    PRIVATE
        ../dpf/distrho
        ../src/Cardinal)

target_compile_definitions(Cardinal
    PUBLIC
        DISTRHO_NAMESPACE=CardinalDISTRHO
        DGL_NAMESPACE=CardinalDGL
        JucePlugin_PreferredChannelConfigurations=8,8
        JUCE_CHECK_MEMORY_LEAKS=0
        JUCE_DISABLE_NATIVE_FILECHOOSERS=1
        JUCE_DISPLAY_SPLASH_SCREEN=0
        JUCE_MODAL_LOOPS_PERMITTED=0
        JUCE_USE_CURL=0
        JUCE_USE_FLAC=0
        JUCE_USE_OGGVORBIS=0
        JUCE_USE_XINERAMA=0
        JUCE_VST3_CAN_REPLACE_VST2=0
        JUCE_ALSA=0
        JUCE_DIRECTSOUND=0
        JUCE_JACK=0
        JUCE_WASAPI=0
        JUCE_WEB_BROWSER=0)

target_link_libraries(Cardinal
    PRIVATE
        juce::juce_audio_utils
        ${STATIC_LIBS_START}
        sPlugins
        sCardinal
        sRack
        carla_host_plugin
        carla_engine_plugin
        carla_plugin
        native_plugins
        audio_decoder
        jackbridge
        lilv
        rtmempool
        water
        ysfx
        zita_resampler
        dgl
        surgedep01
        surgedep02
        surgedep03
        surgedep04
        surgedep05
        surgedep06
        surgedep07
        #surgedep08
        surgedep09
        surgedep10
        libaubio
        libarchive
        libjansson
        libquickjs
        libsamplerate
        libspeexdsp
        libzstd
        ${STATIC_LIBS_END}
        ${GL_LIBRARIES}
        ${DBUS_LIBRARIES}
        -L${LIBLO_LIBRARY_DIRS}
        ${FFTW3F_LIBRARIES}
        ${LIBLO_LIBRARIES}
        ${SNDFILE_LIBRARIES}
        ${X11_LIBRARIES}
        ${XCURSOR_LIBRARIES}
        ${XEXT_LIBRARIES}
        ${XRANDR_LIBRARIES}
        ${EXTRA_LIBS}
        -lmagic
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_warning_flags)
#]]

# FX variant

juce_add_plugin(CardinalFX
    AU_MAIN_TYPE kAudioUnitType_MusicEffect
    COMPANY_COPYRIGHT "GPL-3.0-or-later"
    COMPANY_NAME "DISTRHO"
    COMPANY_WEBSITE "https://github.com/DISTRHO/Cardinal"
    DESCRIPTION "Virtual modular synthesizer plugin"
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    FORMATS ${PLUGIN_FORMATS}
    IS_MIDI_EFFECT FALSE
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT TRUE
    NEEDS_MIDI_OUTPUT TRUE
    PLUGIN_CODE DcnF
    PLUGIN_MANUFACTURER_CODE Dstr
    PRODUCT_NAME "CardinalFX")

target_sources(CardinalFX
    PRIVATE
        CardinalWrapper.cpp)

target_include_directories(CardinalFX
    PRIVATE
        ../dpf/distrho
        ../src/CardinalFX)

target_compile_definitions(CardinalFX
    PUBLIC
        DISTRHO_NAMESPACE=CardinalDISTRHO
        DGL_NAMESPACE=CardinalDGL
        JucePlugin_PreferredChannelConfigurations=2,2
        JUCE_CHECK_MEMORY_LEAKS=0
        JUCE_DISABLE_NATIVE_FILECHOOSERS=1
        JUCE_DISPLAY_SPLASH_SCREEN=0
        JUCE_MODAL_LOOPS_PERMITTED=0
        JUCE_USE_CURL=0
        JUCE_USE_FLAC=0
        JUCE_USE_OGGVORBIS=0
        JUCE_USE_XINERAMA=0
        JUCE_VST3_CAN_REPLACE_VST2=0
        JUCE_ALSA=0
        JUCE_DIRECTSOUND=0
        JUCE_JACK=0
        JUCE_WASAPI=0
        JUCE_WEB_BROWSER=0)

target_link_libraries(CardinalFX
    PRIVATE
        juce::juce_audio_utils
        ${STATIC_LIBS_START}
        sPlugins
        sCardinalFX
        sRack
        carla_host_plugin
        carla_engine_plugin
        carla_plugin
        native_plugins
        audio_decoder
        jackbridge
        lilv
        rtmempool
        water
        ysfx
        zita_resampler
        dgl
        surgedep01
        surgedep02
        surgedep03
        surgedep04
        surgedep05
        surgedep06
        surgedep07
        #surgedep08
        surgedep09
        surgedep10
        libaubio
        libarchive
        libjansson
        libquickjs
        libsamplerate
        libspeexdsp
        libzstd
        ${STATIC_LIBS_END}
        ${GL_LIBRARIES}
        ${DBUS_LIBRARIES}
        -L${LIBLO_LIBRARY_DIRS}
        ${FFTW3F_LIBRARIES}
        ${LIBLO_LIBRARIES}
        ${SNDFILE_LIBRARIES}
        ${X11_LIBRARIES}
        ${XCURSOR_LIBRARIES}
        ${XEXT_LIBRARIES}
        ${XRANDR_LIBRARIES}
        ${EXTRA_LIBS}
        -lmagic
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_warning_flags)

# MIDI variant

juce_add_plugin(CardinalMIDI
    AU_MAIN_TYPE kAudioUnitType_MIDIProcessor
    COMPANY_COPYRIGHT "GPL-3.0-or-later"
    COMPANY_NAME "DISTRHO"
    COMPANY_WEBSITE "https://github.com/DISTRHO/Cardinal"
    DESCRIPTION "Virtual modular synthesizer plugin"
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    FORMATS ${PLUGIN_FORMATS}
    IS_MIDI_EFFECT TRUE
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT TRUE
    NEEDS_MIDI_OUTPUT TRUE
    PLUGIN_CODE DcnM
    PLUGIN_MANUFACTURER_CODE Dstr
    PRODUCT_NAME "CardinalMIDI")

target_sources(CardinalMIDI
    PRIVATE
        CardinalWrapper.cpp)

target_include_directories(CardinalMIDI
    PRIVATE
        ../dpf/distrho
        ../src/CardinalFX)

target_compile_definitions(CardinalMIDI
    PUBLIC
        DISTRHO_NAMESPACE=CardinalDISTRHO
        DGL_NAMESPACE=CardinalDGL
        JucePlugin_PreferredChannelConfigurations=2,2
        JUCE_CHECK_MEMORY_LEAKS=0
        JUCE_DISABLE_NATIVE_FILECHOOSERS=1
        JUCE_DISPLAY_SPLASH_SCREEN=0
        JUCE_MODAL_LOOPS_PERMITTED=0
        JUCE_USE_CURL=0
        JUCE_USE_FLAC=0
        JUCE_USE_OGGVORBIS=0
        JUCE_USE_XINERAMA=0
        JUCE_VST3_CAN_REPLACE_VST2=0
        JUCE_ALSA=0
        JUCE_DIRECTSOUND=0
        JUCE_JACK=0
        JUCE_WASAPI=0
        JUCE_WEB_BROWSER=0)

target_link_libraries(CardinalMIDI
    PRIVATE
        juce::juce_audio_utils
        ${STATIC_LIBS_START}
        sPlugins
        sCardinalFX
        sRack
        carla_host_plugin
        carla_engine_plugin
        carla_plugin
        native_plugins
        audio_decoder
        jackbridge
        lilv
        rtmempool
        water
        ysfx
        zita_resampler
        dgl
        surgedep01
        surgedep02
        surgedep03
        surgedep04
        surgedep05
        surgedep06
        surgedep07
        #surgedep08
        surgedep09
        surgedep10
        libaubio
        libarchive
        libjansson
        libquickjs
        libsamplerate
        libspeexdsp
        libzstd
        ${STATIC_LIBS_END}
        ${GL_LIBRARIES}
        ${DBUS_LIBRARIES}
        -L${LIBLO_LIBRARY_DIRS}
        ${FFTW3F_LIBRARIES}
        ${LIBLO_LIBRARIES}
        ${SNDFILE_LIBRARIES}
        ${X11_LIBRARIES}
        ${XCURSOR_LIBRARIES}
        ${XEXT_LIBRARIES}
        ${XRANDR_LIBRARIES}
        ${EXTRA_LIBS}
        -lmagic
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_warning_flags)

# Synth variant

juce_add_plugin(CardinalSynth
    AU_MAIN_TYPE kAudioUnitType_MusicDevice
    COMPANY_COPYRIGHT "GPL-3.0-or-later"
    COMPANY_NAME "DISTRHO"
    COMPANY_WEBSITE "https://github.com/DISTRHO/Cardinal"
    DESCRIPTION "Virtual modular synthesizer plugin"
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    FORMATS ${PLUGIN_FORMATS}
    IS_MIDI_EFFECT FALSE
    IS_SYNTH TRUE
    NEEDS_MIDI_INPUT TRUE
    NEEDS_MIDI_OUTPUT TRUE
    PLUGIN_CODE DcnS
    PLUGIN_MANUFACTURER_CODE Dstr
    PRODUCT_NAME "CardinalSynth")

target_sources(CardinalSynth
    PRIVATE
        CardinalWrapper.cpp)

target_include_directories(CardinalSynth
    PRIVATE
        ../dpf/distrho
        ../src/CardinalSynth)

target_compile_definitions(CardinalSynth
    PUBLIC
        DISTRHO_NAMESPACE=CardinalDISTRHO
        DGL_NAMESPACE=CardinalDGL
        JucePlugin_PreferredChannelConfigurations=0,2
        JUCE_CHECK_MEMORY_LEAKS=0
        JUCE_DISABLE_NATIVE_FILECHOOSERS=1
        JUCE_DISPLAY_SPLASH_SCREEN=0
        JUCE_MODAL_LOOPS_PERMITTED=0
        JUCE_USE_CURL=0
        JUCE_USE_FLAC=0
        JUCE_USE_OGGVORBIS=0
        JUCE_USE_XINERAMA=0
        JUCE_VST3_CAN_REPLACE_VST2=0
        JUCE_ALSA=0
        JUCE_DIRECTSOUND=0
        JUCE_JACK=0
        JUCE_WASAPI=0
        JUCE_WEB_BROWSER=0)

target_link_libraries(CardinalSynth
    PRIVATE
        juce::juce_audio_utils
        ${STATIC_LIBS_START}
        sPlugins
        sCardinalSynth
        sRack
        carla_host_plugin
        carla_engine_plugin
        carla_plugin
        native_plugins
        audio_decoder
        jackbridge
        lilv
        rtmempool
        water
        ysfx
        zita_resampler
        dgl
        surgedep01
        surgedep02
        surgedep03
        surgedep04
        surgedep05
        surgedep06
        surgedep07
        #surgedep08
        surgedep09
        surgedep10
        libaubio
        libarchive
        libjansson
        libquickjs
        libsamplerate
        libspeexdsp
        libzstd
        ${STATIC_LIBS_END}
        ${GL_LIBRARIES}
        ${DBUS_LIBRARIES}
        -L${LIBLO_LIBRARY_DIRS}
        ${FFTW3F_LIBRARIES}
        ${LIBLO_LIBRARIES}
        ${SNDFILE_LIBRARIES}
        ${X11_LIBRARIES}
        ${XCURSOR_LIBRARIES}
        ${XEXT_LIBRARIES}
        ${XRANDR_LIBRARIES}
        ${EXTRA_LIBS}
        -lmagic
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_warning_flags)
