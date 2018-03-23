# Kepware Plugin Usage

### Introduction
The Kepware plugin is designed to benefit Enterprise-Connect Predix subscribers. It is capable of performing a realtime protocols-exchange for ingress protocols such as MQTT, WebSocket, HTTP, OPC UA/DA, TCP, and several high-performance egress frameworks, e.g. gRPC, supported by Predix EventHub service.

This usage guide assumes that the user has the basic knowledge of Enterprise-Connect operation, and is currently a subscriber to the EC service in Predix. If not, please [checkut our usage doc](https://github.com/Enterprise-connect/ec-misc-docs) as your first step.

### High-Level Network-Comp. Deployment Diagram
![alt text](https://github.build.ge.com/Enterprise-Connect/ec-sdk/blob/beta/plugins/kepware/KepwareCBPlugin.png)

### Simplifying Deployment
The plugin may operate as a standalone app, please reach out to the user group for more details ec-usergroup@ge-developer-cloud.flowdock.com. However, in most industrial use cases, the Enterprise-Connect agent/service is needed to establish a secure tunnel for data-ingestion purposes.

The combination of EC Agent and the plugin is less than 20MB. With the minimum requirement of 128Mb in-memory, you may bridge the data from anywhere in the world into the designated environment.

### Enhanced Security
The plugin performs data-exchange operations via the Enterprise-Connect security network which will maximise the security compatibility and deliver uncompromised performance.

### Step one of three- Configure the plugins.yml
Again assuming that the user has the basic knowledge of Enterprise-Connect operation, and is currently a subscriber to the EC service in Predix. If not, please [checkut our usage doc](https://github.com/Enterprise-connect/ec-misc-docs) as your first step.

```yaml
  kepware:
    status: active
    command: ./main
    in:
      type: mqtt
      config:
        cid: data-ingestion
        usr: <usr>
        pwd: <pwd>
        hst: localhost
        prt: 7883
        tpc: opcData/vacuum
    out:
      type: proto-px
      config:
        sbj: clearwater
        ptc: grpc
        uri: 'event-hub-aws-usw02.data-services.predix.io:443'
        px-header: 'Predix-Zone-Id'
        px-zone: <zone>
        cid: <cid>
        csc: <csc>
        oauth: 'https://<zone>.predix-uaa.run.aws-usw02-pr.ice.predix.io/oauth/token'
        pxy: 'http://PITC-Zscaler-Americas-Cincinnati3PR.proxy.corporate.ge.com:80'

```
