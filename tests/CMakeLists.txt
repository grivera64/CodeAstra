# Enable testing
enable_testing()

# Add individual test executables
add_executable(test_mainwindow
    test_mainwindow.cpp
)

# Add test_tree executable
add_executable(test_tree
    test_tree.cpp
)

# Link the test with the CodeAstra library and necessary Qt libraries
target_link_libraries(test_mainwindow PRIVATE ${TARGET_NAME} Qt6::Widgets Qt6::Test)
target_link_libraries(test_tree PRIVATE ${TARGET_NAME} Qt6::Widgets Qt6::Test)

# Register each test with CTest
add_test(NAME test_mainwindow COMMAND test_mainwindow)
add_test(NAME test_tree COMMAND test_tree)

# Set the runtime output directory for the test executables
set_target_properties(test_mainwindow PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/tests
)
set_target_properties(test_tree PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/tests
)

set_property(SOURCE test_mainwindow.cpp PROPERTY SKIP_AUTOMOC OFF)
set_property(SOURCE test_tree.cpp PROPERTY SKIP_AUTOMOC OFF)

# Include directories for tests
target_include_directories(test_mainwindow PRIVATE ${CMAKE_SOURCE_DIR}/include)
target_include_directories(test_tree PRIVATE ${CMAKE_SOURCE_DIR}/include)
