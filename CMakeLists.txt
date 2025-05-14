
cmake_minimum_required(VERSION 3.10)
project(OrderBookSimulator)
set(CMAKE_CXX_STANDARD 17)
find_package(mongocxx REQUIRED)
find_package(libmongocxx REQUIRED)
add_executable(simulator src/main.cpp src/order_book.cpp)
target_include_directories(simulator PRIVATE include)
target_link_libraries(simulator PRIVATE mongocxx)

include_directories(vendor/Crow/include)
target_link_libraries(simulator PRIVATE pthread)