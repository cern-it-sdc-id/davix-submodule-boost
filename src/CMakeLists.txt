

## boost
if(NOT Boost_FOUND)

FILE(GLOB BOOST_SRC_SYSTEM "${CMAKE_CURRENT_SOURCE_DIR}/system/src/*.cpp")
FILE(GLOB BOOST_SRC_THREAD "${CMAKE_CURRENT_SOURCE_DIR}/thread/src/pthread/*.cpp")
FILE(GLOB BOOST_SRC_PROGOPTS "${CMAKE_CURRENT_SOURCE_DIR}/program_options/src/*.cpp")


LIST(APPEND SRC_BOOST_ALL ${BOOST_SRC_THREAD} ${BOOST_SRC_SYSTEM} ${BOOST_SRC_PROGOPTS})

SET(SRC_BOOST_ALL ${SRC_BOOST_ALL} PARENT_SCOPE)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/../ ")
add_definitions( -DBOOST_THREAD_BUILD_LIB=1)
add_definitions( -DBOOST_THREAD_POSIX )
add_definitions( -fPIC )
add_definitions(-fvisibility=hidden)
add_library(boost_static_internal STATIC ${SRC_BOOST_ALL})

# if the static library is produced, then we need also to install the dependent libraries to be useful
if(STATIC_LIBRARY)
  install(TARGETS boost_static_internal DESTINATION ${LIB_INSTALL_DIR} )
endif()

endif(NOT Boost_FOUND)
