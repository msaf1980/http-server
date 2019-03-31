cmake_minimum_required(VERSION 3.5)

project(test)

include(CTest)



add_executable(test_target test.c)
add_test(NAME test_noArgs COMMAND test_target)
# Add timeout settings for test
set_tests_properties( 
    test_noArgs PROPERTIES
    TIMEOUT 30
    TIMEOUT_AFTER_MATCH "Condition met"
)

#set_target_properties( test_target PROPERTIES EXCLUDE_FROM_ALL 1 EXCLUDE_FROM_DEFAULT_BUILD 1 )
set_tests_properties( test_noArgs PROPERTIES EXCLUDE_FROM_ALL 1 EXCLUDE_FROM_DEFAULT_BUILD 1 )
