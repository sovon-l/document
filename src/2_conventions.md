# Conventions

This is to explain the existing conventions used in the project.

## 1. Instrument

There are three type of conventions.

1. Encoding format - we use the instrument type defined at market_definition.

2. In memory format - we use instrument enum define at (rust) market.

3. String format - we use "{exchange}:{quote}_{base}(-{type})" - where () means optional. without () auto means "-0". The type definitions are as below:

    - "-0" means **spot**
    - "-1" means **_perpetual_ future**
        - "-1_1654693200" means future that **expires** at epoch 1654693200
    - "-2" means perpetual **inverse** future
        - "-2_1654693200"
    - "-3_1654693200_P_20000" means **_put_ option** that **expires** at epoch 1654693200 with a **strike** price 20000
    - "-4_1654693200_C_20000" means **call _inverse_ option** that **expires** at epoch 1654693200 with a **strike** price 20000
    

glossary:

- spot, future, option, strike, call put, expire... go back and study la...

- inverse product means product that calculates at the given pair but settle at quote currency. e.g. you short BTC_USD-2 with volume 50000 USD when the quoted price is 50000, it will take 1 BTC position from your wallet; then when you square off your position at quoted price 25000, you will gain 2 BTC your wallet. I think it is mainly used in short positions.

reference: market:/src/structs/instrument.rs