catkin_add_gtest(test_blockmem_gridmap src/test_blockmem_gridmap.cpp)
target_link_libraries(test_blockmem_gridmap ${catkin_LIBRARIES} ${Boost_LIBRARIES})

catkin_add_gtest(test_cyclic_vec src/test_cyclic_vec.cpp)
target_link_libraries(test_cyclic_vec ${catkin_LIBRARIES} ${Boost_LIBRARIES})

catkin_add_gtest(test_grid_metric_converter src/test_grid_metric_converter.cpp)
target_link_libraries(test_grid_metric_converter ${catkin_LIBRARIES} ${Boost_LIBRARIES})

catkin_add_gtest(test_motion_cache src/test_motion_cache.cpp)
target_link_libraries(test_motion_cache ${catkin_LIBRARIES} ${Boost_LIBRARIES})

if(PLANNER_CSPACE_PERFORMANCE_TESTS)

  catkin_add_gtest(test_blockmem_gridmap_performance src/test_blockmem_gridmap_performance.cpp)
  target_link_libraries(test_blockmem_gridmap_performance ${catkin_LIBRARIES} ${Boost_LIBRARIES})
  set_target_properties(test_blockmem_gridmap_performance PROPERTIES COMPILE_FLAGS "${CMAKE_CXX_FLAGS_RELEASE}") # Force release build for performance test.

else()

  message("To perform performance tests for planner_cspace, use -DPLANNER_CSPACE_PERFORMANCE_TESTS:=ON")

endif()

add_rostest_gtest(test_navigate
  test/navigation_rostest.test
  src/test_navigate.cpp
)
target_link_libraries(test_navigate ${catkin_LIBRARIES})
add_dependencies(test_navigate planner_3d)

add_rostest_gtest(test_navigate_compat
  test/navigation_compat_rostest.test
  src/test_navigate.cpp
)
target_link_libraries(test_navigate_compat ${catkin_LIBRARIES})
add_dependencies(test_navigate_compat planner_3d)

add_rostest_gtest(test_abort
  test/abort_rostest.test
  src/test_abort.cpp
)
target_link_libraries(test_abort ${catkin_LIBRARIES})
add_dependencies(test_abort planner_3d)

add_rostest_gtest(test_preempt
  test/preempt_rostest.test
  src/test_preempt.cpp
)
target_link_libraries(test_preempt ${catkin_LIBRARIES})
add_dependencies(test_preempt planner_3d)
