# Kepware Plugin Usage

### Introduction
The Kepware plugin is designed to benefit Enterprise-Connect Predix subscribers. It is capable of performing a realtime protocols-exchange for ingress protocols such as MQTT, WebSocket, HTTP, OPC UA/DA, TCP, and several high-performance egress frameworks, e.g. gRPC, supported by Predix EventHub service.

### High-Level Network-Comp. Deployment Diagram
![alt text](https://github.build.ge.com/Enterprise-Connect/ec-sdk/blob/beta/plugins/kepware/KepwareCBPlugin.png)

### Simplifying Deployment
The plugin may operate as a standalone app, please reach out to the user group for more details ec-usergroup@ge-developer-cloud.flowdock.com. However, in most industrial use cases, the Enterprise-Connect agent/service is needed to establish the secure tunnel for many data-ingestion purposes.

The commination of a pair of EC Agent and the plugin is less than 20MB, with the minimum requirement of 128Mb in-memory, you may bridge the data from anywhere in the world into the designated environment.

### Enhanced Security
The plugin operates data-transmitting via the Enterprise-Connect security network which will maximise the security compatibility without a potential setback towards it's operation performance.


