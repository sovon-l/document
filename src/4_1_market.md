# Market

The purpose of product "Market" is to deliver market data only. Market data has a variety of usage, including but not limited to: synthesizing algo orders, generating signals, initiating trade strategies, forming data lake. Although a single source of truth for market data seems preferrable, but sometimes it is not a part of originating business requirement.

To operate this module, some key points have to be observed:

- `/src/api/` It expects other component to use API inside this folder to access data from market component. Specifically, `market_listener` expect people to implement the trait there and process in inherited functions when market data arrives.

- `/src/structs/` lists some common public data structures that might be used by other components.

- `/src/data/` includes the core of market component - the connectivity to different exchanges. `/src/data/controller.rs` includes an function `work()` to allow user initiate access to exchange venues, start crawling data, and passing the data to `sender`. It is currently a crossbeam channel, but is subject to improvement (e.g. `impl Sink`).

- `/src/utils/` stores function that does not directly serve the purpose of Market but is essential, and is reduced into reuseable patterns.

For the first demonstration purpose, this component is containerized and is ready to be run as a pod of k8s - using zme sbe for data transfer inside the cluster.

- `/Dockerfile` includes how to create the image

- `/deployment/` is the files that make this into a k8s component. As you see I have tried hosting it under a k8s in my domain name but that is really very very costly for development purpose, but it worked.

There are some other things that might need to be looked out for.

- `/market_definition` (git submodule) does not directly affect the compileable source code of Market, but indeed fixed the version of SBE encoding used by fixing a commit of that repo.

- `/proper_market_api` (cargo submodule) is actually a generated code base from `market_definition`. It is most likely not required to examine, but the SBE code generator is sometimes buggy and need you to fix 0.1% of its work to coerce with rust syntax. If you didnt touch it, this is ignorable.