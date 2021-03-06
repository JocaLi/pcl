set(SUBSYS_NAME global_tests)
set(SUBSYS_DESC "Point cloud library global unit tests")

set(DEFAULT OFF)
set(build TRUE)
PCL_SUBSYS_OPTION(build "${SUBSYS_NAME}" "${SUBSYS_DESC}" ${DEFAULT} "${REASON}")
PCL_SUBSYS_DEPEND(build "${SUBSYS_NAME}" DEPS ${SUBSYS_DEPS} OPT_DEPS ${OPT_DEPS})

if(build)

    find_package(Gtest REQUIRED)
    include_directories(SYSTEM ${GTEST_INCLUDE_DIRS} ${GTEST_SRC_DIR})

    add_library(pcl_gtest STATIC ${GTEST_SRC_DIR}/src/gtest-all.cc)

    if(MSVC11) # VS2012 doesn't correctly support variadic templates yet
        add_definitions("-D_VARIADIC_MAX=10")
    endif()

    enable_testing()
    add_custom_target(tests "${CMAKE_CTEST_COMMAND}" "-V" VERBATIM)

    add_subdirectory(2d)
    add_subdirectory(common)
    add_subdirectory(features)
    add_subdirectory(filters)
    add_subdirectory(geometry)
    add_subdirectory(io)
    add_subdirectory(kdtree)
    add_subdirectory(keypoints)
    add_subdirectory(people)
    add_subdirectory(octree)
    add_subdirectory(outofcore)
    add_subdirectory(recognition)
    add_subdirectory(registration)
    add_subdirectory(search)
    add_subdirectory(surface)
    add_subdirectory(segmentation)
    add_subdirectory(sample_consensus)
    add_subdirectory(visualization)

endif()
