# Market Data Feed Handler (C++)

A high-performance C++-based market data feed handler for high-frequency trading (HFT), processing 1M+ ticks/sec with <500ns latency. Utilizes lock-free queues, zero-copy JSON parsing, and an in-memory order book with `std::priority_queue` and `boost::asio`.

## Prerequisites
- **OS**: macOS (tested on macOS Ventura)
- **Tools**: CMake 3.10+, g++ or clang++ (C++17), Homebrew
- **Dependencies**:
  - Boost (`boost::asio` for WebSocket)
  - simdjson (JSON parsing)
  - spdlog (logging)
  - Google Test (unit testing)
  - Crow (REST API)
- **Optional**: AWS account for deployment

## Setup
1. **Install Dependencies**:
   ```bash
   brew install cmake gcc boost simdjson spdlog googletest
   ```
2. **Clone Crow**:
   ```bash
   git clone https://github.com/CrowCpp/Crow.git vendor/Crow
   ```
3. **Clone Repository**:
   ```bash
   git clone https://github.com/rbandara/market-data-feed-cpp.git
   cd market-data-feed-cpp
   ```

## Build
1. **Create Build Directory**:
   ```bash
   mkdir build && cd build
   ```
2. **Run CMake**:
   ```bash
   cmake .. -DCMAKE_BUILD_TYPE=Debug
   ```
3. **Compile**:
   ```bash
   make
   ```

## Run
- **Start the Application**:
  ```bash
  ./simulator
  ```
- **Test the API**:
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{"id":"1","type":"buy","price":100.5,"volume":10}' http://localhost:8080/order
  curl http://localhost:8080/trades
  ```

## Testing
Unit tests for the `matchOrders()` method verify basic matching, partial matches, price mismatches, price-time priority, and empty book scenarios using Google Test.

- **Run Tests**:
  ```bash
  ./tests
  ```
- **Expected Output**:
  ```
  [==========] Running 5 tests from 1 test suite.
  [----------] 5 tests from OrderBookTest
  [ RUN      ] OrderBookTest.BasicMatch
  [       OK ] OrderBookTest.BasicMatch (0 ms)
  [ RUN      ] OrderBookTest.PartialMatch
  [       OK ] OrderBookTest.PartialMatch (0 ms)
  [ RUN      ] OrderBookTest.NoMatchPrice
  [       OK ] OrderBookTest.NoMatchPrice (0 ms)
  [ RUN      ] OrderBookTest.PriceTimePriority
  [       OK ] OrderBookTest.PriceTimePriority (0 ms)
  [ RUN      ] OrderBookTest.EmptyBook
  [       OK ] OrderBookTest.EmptyBook (0 ms)
  [----------] 5 tests from OrderBookTest (0 ms total)
  [==========] 5 tests from 1 test suite ran. (0 ms total)
  [  PASSED  ] 5 tests.
  ```

## Deployment
- **Dockerize**:
  ```bash
  docker build -t market-data-feed-cpp .
  docker run -p 8080:8080 market-data-feed-cpp
  ```

## Project Structure
```
market-data-feed-cpp/
├── include/
│   └── order_book.hpp
├── src/
│   ├── main.cpp
│   └── order_book.cpp
├── test/
│   └── test_order_book.cpp
├── vendor/
│   └── Crow/
├── CMakeLists.txt
├── Dockerfile
├── deploy.sh
└── README.md
```

## Contributing
- Fork the repository, create a feature branch, and submit a pull request.
- Run tests before committing: `cd build && ./tests`.

## License
MIT License
