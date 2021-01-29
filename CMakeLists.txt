cmake_minimum_required(VERSION 3.9)
project(mylib VERSION 0.0.1 DESCRIPTION "mylib description")
add_library(mylib SHARED
    sources/compute.cpp)
set_target_properties(mylib PROPERTIES VERSION ${PROJECT_VERSION})
