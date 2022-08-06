# Market

Market is aimed to be a portable mini product that can be either pluged into another product as an attached service, or run separately as a microservice.

From general design philosophy, this product [is designed to be as simple as possible. It is not a full blown market data service, but a simple data source that can be used to build other products.](## "copilot says")

## As an attached service

`market::data::controller::work(..)` is the main controller of this service. It will handle a state separately, allow you to refresh connections in the state each time calling it, and return the data to sender. Sender [is currently a crossbeam channel, but it is subject to change to a more general trait.](## "copilot says")

## As a separate microservice

Currently an example `cargo run --example async_publisher` is provided. It digests json request with instrumenbt list from `localhost:7800` and pass into work function. [It is a simple example of how to use market as a microservice.](## "copilot says")