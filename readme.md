# Order Book Simulator
A high-performance trading simulator built in Go to replicate a financial exchange’s order book, matching buy and sell orders in real time with <1ms latency.

## Motivation
This project was inspired by the need for low-latency, scalable trading systems in financial markets, drawing on my 20 years of experience building regulatory-compliant platforms (e.g., at Wells Fargo). The simulator leverages Go’s goroutines and channels to process 10,000+ orders/sec, showcasing concurrency and performance optimization. Deployed on AWS ECS, it demonstrates end-to-end system design, from order matching to cloud deployment, addressing real-world challenges in fintech.

## Key Features
- Concurrent order matching using goroutines and channels.
- Thread-safe order book updates with `sync.Mutex`.

## Tech Stack
- Go, `net/http`, `sync`
- AWS ECS, Docker
- MongoDB for order persistence