cmake_minimum_required(VERSION 3.2)

project(fdeep)
include(CMake/CPM.cmake)

if(NOT TARGET Threads)
    find_package(Threads REQUIRED)
endif()

CPMAddPackage(
        NAME FUNCTIONALPLUS
        GITHUB_REPOSITORY Dobiasd/FunctionalPlus
        GIT_TAG origin/master)
if(NOT TARGET FunctionalPlus::fplus)
  find_package(FunctionalPlus CONFIG REQUIRED)
endif()

CPMAddPackage(
        NAME EIGEN3
        GITLAB_REPOSITORY libeigen/eigen
        GIT_TAG origin/master)
if(NOT TARGET Eigen3::Eigen)
    find_package(Eigen3 CONFIG REQUIRED)
endif()

CPMAddPackage(
        NAME JSON
        GITHUB_REPOSITORY eupston/json
        GIT_TAG origin/develop)
if(NOT TARGET nlohmann_json)
    find_package(nlohmann_json CONFIG REQUIRED)
endif()

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} INTERFACE $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>)

target_link_libraries(${PROJECT_NAME} INTERFACE
        Threads::Threads
        nlohmann_json
        FunctionalPlus::fplus
        Eigen3::Eigen
    )