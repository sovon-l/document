# gateway

Gateway also aim to be a portable mini product [that can be either pluged into another product as an attached service, or run separately as a microservice.](## "copilot says") However, contrastly gateway is more complicated as it needs to store and manage states of the orders at the exchange venues, and translate them into a unified format for other products to use.

## Internal communication design

We will need an internal communicator to allow different parts of gateway communicate the states of orders. Currently implementing a in-memory design with interfaces (traits) that has connection pool design in mind.

## Decomposition

### Internal

[Internally Gateway should be decomposed into 4 parts:](## "copilot says")

#### Order Executor

[Order executor is the part that actually send orders to the exchange venue. It should be able to handle multiple orders at the same time, and should be able to handle multiple exchange venues at the same time. It should also be able to handle multiple accounts at the same time.](## "copilot says") It's job is place [orders and cancel orders.](## "copilot says") We need to note that hot path [of this part is very important, and should be optimized as much as possible.](## "copilot says")

#### State Listener

[State listener is the part that listen to the state of the orders at the exchange venue. It's job is to listen to the state of the orders and update the state of the orders.](## "copilot says") For accounting purpose, we will also need to store [the state of the orders](## "copilot says") into e.g. a SQL database.

#### Order Manager

Order manager is a part the fires scheduled events on inactive open orders, to keep order last update [time fresh and prevent](## "copilot says") situations like message lost [or exchange venue server crash.](## "copilot says")

#### Order Actioner

This part is responsible for [taking actions](## "copilot says") that does not have a hot path requirement. For example, requesting latest order info. This can either be triggered by order manager[, or by other products.](## "copilot says")

### External

[Externally Gateway should be decomposed into 2 parts:](## "copilot says")

#### Input

Input is separated into hot path and non hot path. Hot path means those order placing and cancelling, and should be as [fast as possible. Non hot path means those order info requesting, and should be as reliable as possible.](## "copilot says")

#### [Output](## "copilot says")

[Output is](## "copilot says") also [separated into hot path and non hot path. Hot path means](## "copilot says") the status of the order and should be as [fast as possible. Non hot path means the](## "copilot says") transaction info [and should be as reliable as possible.](## "copilot says")