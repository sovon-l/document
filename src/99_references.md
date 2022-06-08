# References

This is a non-exhaustive list of references that might help to understand the project.

## 1. SBE: Simple Binary Encoding

This is expected to be one of the fastest encoding/decoding scheme for data transfer since it expects its format to fit the memory directly. Some references below:

- [Source Code](https://github.com/real-logic/simple-binary-encoding)
- [How to use](https://github.com/real-logic/simple-binary-encoding/wiki/Sbe-Tool-Guide)
- [How to write definition files](https://github.com/real-logic/simple-binary-encoding/wiki/FIX-SBE-XML-Primer)
- [FIX message definition sample](https://github.com/real-logic/simple-binary-encoding/blob/master/sbe-benchmarks/src/main/resources/fix-message-samples.xml)

## 2. ZMQ: Not a message queue

The usual MQ products are actually a separate running process that manage the messages. ZMQ although has a queue in its runtime, should still yield a lower transferring latency than having a MQ product between our components. This could help us clear out the flow that requires absolute speed (from receiving market data to place order).

- [z guide](https://zguide.zeromq.org/)