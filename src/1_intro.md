# Introduction

This project aims to create a low latency trading system in rust. By taking advantage of rust package manager, I expect this project could easily assemble different parts of the trading system into a single binary and provide optimal solutions in every scenario.

The (temporary) project structure will be listed below:

## Market

This is the most readily available module. By passing the instruments to it as arguments, you could get a steady stream of data. The stream of data is published in anyway defined in the messenger crate: Either in memory (crossbeam channel / bus), or through zmq and serialization.

This is expected to be deployed at multiple locations.

### Market Storer

This is a simple golang component that demonstrate the use of zmq sbe transfer on market data, available for benchmarking usage.

## Gateway

This manages connection directly to the exchange. Besides, it also contains some critical role such as synthesizing orders. One example is if the exchange doesn't support stop loss order, gateway will need to listen to the instrument market data and play after trigger condition occurs. There are more orders to synthesize, like adaptive midprice / OCO / OTO etc.

As the example suggests, gateway is expected to be compiled with market component (as gateway should be the nearest component to exchange venue) to react on price or other market actions.

## OEPMS(?)

This is the (virtual) component(s) that expects to do several jobs:

- Split the strategies (multi-tenant). This helps multiple strategies could act on same fund pool.
- Deposit / Withdraw fund for the strategies.
- Internal order matching. This could help our strategies to save commission fees from acting at exchange venue.
- Securities lending?
- Risk management? Eyes on leverages / loan value etc
- Issue command to transfer funds between exchange venues?

This is still at pre-design stage.

## Strategies

As its name, the real strategy on market. At this stage, I'm open to selections like python notebook or anything that allow more strategists joining the trading system and work together.

This product could expect a market component assisting it. Since there is (great) possibility that rust is not used here, zmq sbe support is required (but could be wrapped into a library).