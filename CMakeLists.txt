cmake_minimum_required(VERSION 3.0.2)
include(ProcessorCount)
project(slic3r_wrapper)

find_package(catkin REQUIRED COMPONENTS)

add_subdirectory(src)

ProcessorCount(NPROC)
catkin_package(
    #INCLUDE_DIRS include    
    INCLUDE_DIRS 
        xs/src
        xs/src/libslic3r
        xs/src/libslic3r/IO
    LIBRARIES 
        libslic3r 
        admesh
        BSpline
        clipper
        expat
        polypartition
        poly2tri
        ZipArchive
        miniz
    #CATKIN_DEPENDS ${LIBSLIC3R_DEPENDS}
)

install(TARGETS 
            slic3r
            libslic3r 
            admesh
            BSpline
            clipper
            expat
            polypartition
            poly2tri
            ZipArchive
            miniz
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

#here we copy all headers as plain list to ${CATKIN_PACKAGE_INCLUDE_DESTINATION}/..
#it would be better to specify what include folder catkin packge actually exports
install(
        DIRECTORY 
            xs/src/
        DIRECTORY 
            xs/src/libslic3r/
        DIRECTORY 
            xs/src/libslic3r/IO/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}/..
        FILES_MATCHING 
        PATTERN "*.h" 
        PATTERN "*.hpp"
)        
