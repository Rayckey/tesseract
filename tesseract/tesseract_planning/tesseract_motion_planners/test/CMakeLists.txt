find_package(GTest REQUIRED)
find_package(tesseract_support REQUIRED)

# Descartes Tesseract Kinematics Test
add_executable(${PROJECT_NAME}_descartes_kin_unit descartes_tesseract_kinematics_tests.cpp)
target_link_libraries(${PROJECT_NAME}_descartes_kin_unit PRIVATE GTest::GTest GTest::Main ${PROJECT_NAME}_descartes tesseract::tesseract_support)
tesseract_target_compile_options(${PROJECT_NAME}_descartes_kin_unit PRIVATE)
tesseract_clang_tidy(${PROJECT_NAME}_descartes_kin_unit)
tesseract_code_coverage(${PROJECT_NAME}_descartes_kin_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
tesseract_gtest_discover_tests(${PROJECT_NAME}_descartes_kin_unit)
add_dependencies(${PROJECT_NAME}_descartes_kin_unit ${PROJECT_NAME}_descartes)
add_dependencies(run_tests ${PROJECT_NAME}_descartes_kin_unit)

# OMPL Planning Test/Example Program
add_executable(${PROJECT_NAME}_ompl_unit ompl_planner_tests.cpp)
target_link_libraries(${PROJECT_NAME}_ompl_unit PRIVATE ${Boost_LIBRARIES} GTest::GTest GTest::Main ${PROJECT_NAME}_ompl tesseract::tesseract_support trajopt::trajopt)
target_include_directories(${PROJECT_NAME}_ompl_unit SYSTEM PRIVATE ${Boost_INCLUDE_DIRS})
tesseract_target_compile_options(${PROJECT_NAME}_ompl_unit PRIVATE)
tesseract_clang_tidy(${PROJECT_NAME}_ompl_unit)
tesseract_code_coverage(${PROJECT_NAME}_ompl_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
tesseract_gtest_discover_tests(${PROJECT_NAME}_ompl_unit)
add_dependencies(${PROJECT_NAME}_ompl_unit ${PROJECT_NAME}_ompl)
add_dependencies(run_tests ${PROJECT_NAME}_ompl_unit)

# OMPL Constrained Planning Test/Example Program
if(NOT OMPL_VERSION VERSION_LESS "1.4.0")
  add_executable(${PROJECT_NAME}_ompl_constrained_unit ompl_constrained_planner_tests.cpp)
  target_link_libraries(${PROJECT_NAME}_ompl_constrained_unit PRIVATE ${Boost_LIBRARIES} GTest::GTest GTest::Main ${PROJECT_NAME}_ompl tesseract::tesseract_support trajopt::trajopt)
  target_include_directories(${PROJECT_NAME}_ompl_constrained_unit SYSTEM PRIVATE ${Boost_INCLUDE_DIRS})
  tesseract_target_compile_options(${PROJECT_NAME}_ompl_constrained_unit PRIVATE)
  tesseract_clang_tidy(${PROJECT_NAME}_ompl_constrained_unit)
  tesseract_code_coverage(${PROJECT_NAME}_ompl_constrained_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
  tesseract_gtest_discover_tests(${PROJECT_NAME}_ompl_constrained_unit)
  add_dependencies(${PROJECT_NAME}_ompl_constrained_unit ${PROJECT_NAME}_ompl)
  add_dependencies(run_tests ${PROJECT_NAME}_ompl_constrained_unit)
endif()

# TrajOpt Planner Tests
add_executable(${PROJECT_NAME}_trajopt_unit trajopt_planner_tests.cpp)
target_link_libraries(${PROJECT_NAME}_trajopt_unit PRIVATE GTest::GTest GTest::Main ${PROJECT_NAME}_trajopt tesseract::tesseract_support)
tesseract_target_compile_options(${PROJECT_NAME}_trajopt_unit PRIVATE)
tesseract_clang_tidy(${PROJECT_NAME}_trajopt_unit)
tesseract_code_coverage(${PROJECT_NAME}_trajopt_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
tesseract_gtest_discover_tests(${PROJECT_NAME}_trajopt_unit)
add_dependencies(${PROJECT_NAME}_trajopt_unit ${PROJECT_NAME}_trajopt)
add_dependencies(run_tests ${PROJECT_NAME}_trajopt_unit)

# Descartes Planner Tests
add_executable(${PROJECT_NAME}_descartes_unit descartes_planner_tests.cpp)
target_link_libraries(${PROJECT_NAME}_descartes_unit PRIVATE GTest::GTest GTest::Main ${PROJECT_NAME}_descartes tesseract::tesseract_support tesseract::tesseract_kinematics_opw)
tesseract_target_compile_options(${PROJECT_NAME}_descartes_unit PRIVATE)
tesseract_clang_tidy(${PROJECT_NAME}_descartes_unit)
tesseract_code_coverage(${PROJECT_NAME}_descartes_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
tesseract_gtest_discover_tests(${PROJECT_NAME}_descartes_unit)
add_dependencies(${PROJECT_NAME}_trajopt_unit ${PROJECT_NAME}_descartes)
add_dependencies(run_tests ${PROJECT_NAME}_descartes_unit)

# OMPL TrajOpt Planning Test
# Note: Disabling this test because ompl is not deterministic and must be tuned to provide decent seed trajectories for trajopt.
#add_executable(${PROJECT_NAME}_ompl_trajopt_unit ompl_trajopt_planner_test.cpp)
#target_link_libraries(${PROJECT_NAME}_ompl_trajopt_unit PRIVATE ${Boost_LIBRARIES} GTest::GTest GTest::Main ${PROJECT_NAME}_ompl_trajopt_freespace tesseract::tesseract_support)
#target_include_directories(${PROJECT_NAME}_ompl_trajopt_unit SYSTEM PRIVATE ${Boost_INCLUDE_DIRS})
#tesseract_target_compile_options(${PROJECT_NAME}_ompl_trajopt_unit PRIVATE)
#tesseract_clang_tidy(${PROJECT_NAME}_ompl_trajopt_unit)
#tesseract_code_coverage(${PROJECT_NAME}_ompl_trajopt_unit ALL EXCLUDE ${COVERAGE_EXCLUDE})
#tesseract_gtest_discover_tests(${PROJECT_NAME}_ompl_trajopt_unit)
#add_dependencies(${PROJECT_NAME}_ompl_trajopt_unit ${PROJECT_NAME}_ompl_trajopt_freespace)
#add_dependencies(run_tests ${PROJECT_NAME}_ompl_trajopt_unit)
