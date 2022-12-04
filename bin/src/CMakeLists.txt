  cmake_minimum_required(VERSION 3.10)
  project(developersworkspace_server_client)

  set(CMAKE_CXX_STANDARD 11)
  set(BUILD_SHARED_LIBS ON CACHE STRING "Link to shared libraries by default.")

  # Set entry
  set(SOURCE_FILES main.cpp)

  # Set exit
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ~/server/release.tmp)

  # Create the executable

  add_executable(start ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)

  # Link the libraries

  ## AWSSDK ###############################################################
  #------------------------------------------------------------------------
  set(CMAKE_PREFIX_PATH /usr/bin/deps/aws-sdk/bin/lib/cmake/AWSSDK)

  find_package(AWSSDK)

  message(STATUS "AWSSDK INCLUDE DIRECTORY: ${AWSSDK_INCLUDE_DIRS}")
  target_include_directories(start PUBLIC ${AWSSDK_INCLUDE_DIRS})

  message(STATUS "AWSSDK LINKING LIBRARIES: ${AWSSDK_LINK_LIBRARIES}")
  target_link_libraries(start ${AWSSDK_LINK_LIBRARIES})

  unset(CMAKE_PREFIX_PATH)
  #------------------------------------------------------------------------

  ## Luajit ###############################################################
  #------------------------------------------------------------------------
  message(STATUS "LUAJIT INCLUDE DIRECTORY: /usr/bin/deps/luajit/installation/include/luajit-2.1")
  target_include_directories(start PUBLIC /usr/bin/deps/luajit/installation/include/luajit-2.1)

  message(STATUS "LUAJIT LINKING LIBRARIES: /usr/bin/deps/luajit/installation/lib/libluajit-5.1.so.2.1.0")
  target_link_libraries(start /usr/bin/deps/luajit/installation/lib/libluajit-5.1.so.2.1.0)

  #------------------------------------------------------------------------

  ## PNEUMALIB ############################################################
  #------------------------------------------------------------------------
  message(STATUS "LINKING FRAMEWORK")
  target_include_directories(start PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
  #------------------------------------------------------------------------
