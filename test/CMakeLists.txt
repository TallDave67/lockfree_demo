cmake_minimum_required(VERSION 3.5)
project(lockfree_test)

set(CMAKE_CXX_STANDARD 20) 
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_compile_options("-O0")

enable_testing()
find_package(Threads REQUIRED)

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_executable(exchange_buffer_test
    main.cpp
    exchange_buffer_test.cpp
)

target_link_libraries(exchange_buffer_test gtest_main ${CMAKE_THREAD_LIBS_INIT} )

add_executable(exchange_buffer_stresstest
    main.cpp
    exchange_buffer_stresstest.cpp
)

target_link_libraries(exchange_buffer_stresstest gtest_main ${CMAKE_THREAD_LIBS_INIT} )

add_executable(sync_counter_stresstest
    main.cpp
    sync_counter_stresstest.cpp
    ../src/sync_counter.cpp
#this is not nice but will do for now
)

target_link_libraries(sync_counter_stresstest gtest_main ${CMAKE_THREAD_LIBS_INIT} )