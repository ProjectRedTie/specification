# The Purpose

Ever since the dawn of the Minecraft proxy in 2012, most proxies have been following the same fundamental formula:

* A player connects to the proxy.
* The proxy authenticates the player.
* The proxy establishes a separate connection to the server the player will be connected to.

The communication between the proxy and the server has always been using the regular Minecraft protocol. This was good for initial rapid prototyping.

However, with the advent of networks with tens of thousands of players and Minecraft servers capable of holding thousands of players at once, there are clear inefficiencies in this system. Over time, there have been approaches to improve the situation. For instance, the Velocity project has invested into using faster compression libraries and more recently optimizing memory copies in its pipelines, but it is clear that these half-measures are not enough. Project Red Tie aims to provide a protocol that, with close communication between servers and proxies, allows servers to service many thousands of players on a proxy with just as many, if not much more.

We aim to provide a protocol that works not just for thousands of players but also hundreds of players or even just tens of players. The fundamental principles do not change depending on player count.
