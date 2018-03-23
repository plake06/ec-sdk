# Kepware Plugin Usage

### Introduction
The Kepware plugin is designed for Enterprise-Connect Predix subscribers, and is capable of performing a realtime protocols-exchange for ingress protocols such as MQTT, WebSocket, HTTP, OPC UA/DA, TCP, and several high-performance egress frameworks, such as gRPC, supported by Predix EventHub service.

### High-Level Network-Comp. Deployment Diagram
![alt text](https://github.build.ge.com/Enterprise-Connect/ec-sdk/blob/beta/plugins/kepware/KepwareCBPlugin.png)

### Simplifying Deployment
The plugin can operate as standalone app (please reach out to the user group for more details ec-usergroup@ge-developer-cloud.flowdock.com) . Howevr in most industrial use cases, you would need Enterprise-Connect agent/service to establish the secure tunnel for many data-ingestion purposes.
