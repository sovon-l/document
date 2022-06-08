# Store live data to influx db

This guides you to build a local simple raw data storage solution from live data of supported crypto exchange venue to a local influxdb. These are the rough guidelines:

Prereq:
- Linux environment (wsl2 or real linux)
- influxdb2 installation (I personally suggest a k3s with helm installing bitnami/influxdb)
- rust installation through rustup (I use 1.61)
- go installation (I use 1.18)

Procedure:
1. `cargo run --example async_publisher` at market:/

    It might fail compilation and require you to install sth for libzmq or libczmq-dev sth like that. follow the instructions on compiler or zmq website to proceed
2. `go run .` at market_storer:/

    Remember to pass correct environment variable to configure market_storer connect to influxdb2. read market_storer:/env_var.go
3. `curl localhost:7800 -d '["binance:btc_usdt","binance:eth_usdt"]' -H "Content-Type: application/json"`
4. Verify there is data by observing log of market_storer. There should have no more warning message "no point to influx2".
5. Explore the data in your influxdb2! You may also optionally install grafana and configure to view influxdb2 with influxdb1 sql-like syntax.

