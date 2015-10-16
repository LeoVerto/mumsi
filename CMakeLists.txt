cmake_minimum_required(VERSION 3.0.0)
project(mumsi)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

INCLUDE(FindPkgConfig)
find_package(Boost COMPONENTS system unit_test_framework program_options filesystem REQUIRED)
find_package(PkgConfig REQUIRED)

pkg_check_modules(OPUS "opus")
pkg_check_modules(PJSIP "libpjproject")
pkg_check_modules(LOG4CPP "log4cpp")
pkg_check_modules(SNDFILE "sndfile")


include_directories(${OPUS_INCLUDE_DIRS})
include_directories(${PJSIP_INCLUDE_DIRS})
include_directories(${LOG4CPP_INCLUDE_DIRS})
include_directories(${SNDFILE_INCLUDE_DIRS})
include_directories(libmumble)

link_directories(libmumble)

set(SOURCE_FILES
        PjsuaCommunicator.cpp
        PjsuaCommunicator.hpp
        MumbleCommunicator.cpp
        MumbleCommunicator.hpp
        ISamplesBuffer.hpp)

#set(TEST_SOURCE_FILES
#        SoundSampleQueueTest.cpp
#)

add_executable(mumsi ${SOURCE_FILES} main.cpp)
target_link_libraries(mumsi ${OPUS_LIBRARIES})
target_link_libraries(mumsi ${PJSIP_LIBRARIES})
target_link_libraries(mumsi ${LOG4CPP_LIBRARIES})
target_link_libraries(mumsi ${SNDFILE_LIBRARIES})
target_link_libraries(mumsi ${Boost_LIBRARIES})
target_link_libraries(mumsi mumble)

#add_executable(mumsi_test ${SOURCE_FILES} ${TEST_SOURCE_FILES} test_main.cpp)
#target_link_libraries(mumsi_test ${OPUS_LIBRARIES})
#target_link_libraries(mumsi_test ${PJSIP_LIBRARIES})
#target_link_libraries(mumsi_test ${LOG4CPP_LIBRARIES})
#target_link_libraries(mumsi_test ${SNDFILE_LIBRARIES})
#target_link_libraries(mumsi_test ${Boost_LIBRARIES})
#target_link_libraries(mumsi_test mumble)