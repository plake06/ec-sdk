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

### Step one of Four- Configure the plugins.yml
Again assuming that the user has the basic knowledge of Enterprise-Connect operation, and is currently a subscriber to the EC service in Predix. If not, please [checkut our usage doc](https://github.com/Enterprise-connect/ec-misc-docs) as your first step.

The following plugins.yml file requires to be presented in the same directory of the agent/plugin.

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

#### Ingress
There are several types of protocols supported by this plugin. Currently it's pre-set to MQTT for the beta testing. Pay more attention on the tpc (Topic) configuration, this needs to match your topic which setup in the MQTT broker.

#### Egress
Currently we support gRPC and Predix UAA. You may need to set the pxy (proxy) if you're to deploy this plugin in a onprem/vpn network.

### Step two of Four- Setup the agent for the Ingress traffic
Please verefy your network environment to decide whether the pxy (Proxy) makes sense for your agent deployment.

```bash
c:\> windows_var.exe -mod server \
       -aid <agent Id A> \
       -hst wss://example-gateway.run.ice.predix.io/agent \
       -rht 10.10.10.10 \
       -rpt 1883 \
       -cid <client id> \
       -csc <client secret> \
       -oa2 https://<you UAA uri>/oauth/token \
       -dur 300 \
       -dbg \
       -hca 7990 \
       -shc \
       -zon <your service zone id> \
       -sst <EC service uri> \
       -pxy http://PITC-Zscaler-Americas-Cincinnati3PR.proxy.corporate.ge.com:80

```

### Step three of Four- Setup the agent for the Egress traffic
```bash
c:\> windows_var.exe -mod client \
        -aid <agent Id B> \
        -hst wss://example-gateway.run.ice.predix.io/agent \
        -lpt 7883 \
        -tid <agent Id A> \
        -oa2 https://<your UAA>/oauth/token \
        -cid <client_id> \
        -csc <client secret> \
        -shc \
        -dur 300 \
        -dbg \
        -pxy http://PITC-Zscaler-Americas-Cincinnati3PR.proxy.corporate.ge.com:80

```
