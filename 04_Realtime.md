# Realtime
## MQTT
Broker kan overal gehost worden
- Cloud
- VM
- Docker
- ...

### MQTT Broker
Centrale verbinding.
Enkel berichtjes transporteren.

**Unmanaged services**
Eigen MQTT service

**Unmanaged services**
Amazon IoT, Google Cloud IoT, Azure IoT Hub

### MQTT
Message Queueing Telematry Transport

Machine 2 Machine (M2M) data transfer protocol

Doel:
- Vanop een device naar de cloud.
- Van de cloud naar een ander device sturen.
- Communicatie tussen machines (M2M)

Pro's
- Lightweight
- Bidirectioneel
- Standaard (v3.1.1)
- Gemakkelijk

### Pub/Sub
- **Pub**lishing/**Sub**scribing protocol
- **Broker** is the central handler for the clients
- One or more clients subscribe for a topic
- One or more clients can publish messages on a topic
- Pub/Sub does not know eachother. No IP addresses, ports, location...
- Pub/Sub can happen while other devices are disconnected.

### Brokers
- Mosquitto
- HiveMQ
- Apache ActiveMQ
- RabbitMQ
- Mosca
- RSMB
- WebsphereMQ/IBM MQ
- **Aedes** - NodeJS

### Topics
- Broker has a **Topic** or **Subject**
  - howest/kwe/a/sensors/temperature
- Devices have a subscription on one or more topics

![Single-level wildcard](../images/5256edd76b7dd53eb715b9978a8746c39ba2a9c61ad5aca294d0dea51fd5f302.png)  
![Mutli-level wildcard](../images/837ffcb38e9d88769f38c159ce4a58116ea5e0fcc892f903dfb48012f51b0c88.png)  

### Quality of Service (QoS)
0. Fire And Forget (At most once)
1. Delivered at least once
  - Will be resent until the sender gets an ack.
  - Duplicates can occur.
2. Delivered exactly once
  - More overhead

### Payload
Free choice: JSON, XML, CSV...

No standard: needs documentation!

## Websockets
If we want to capture realtime data, without having to ask for it, we can use websockets.

Een continue 'open' connectie waar de data van & naar kan verstuurd worden, zonder nood aan specifieke requests.

### What are Websockets?
- Websocket is a **networkprotocol** which offers **full-duplex communication** over TCP.
- A connection over **ws://** or **wss://** *i.p.v. http://*
- A special HTTP-request is sent with the 'connection: upgrade' option to the open websocket.
  - Server: 101 Switching protocols
  - Now communication can be sent without HTTP, trough **messages**


### Socket.IO
Implementatie die werkt op basis van Websockets.

Makkelijk socket applicatie opzetten.

Connectie is hetzelfde, welke programmeertaal dan ook.

Met **emit** kunnen we objecten sturen als payload, samen met een custom eventname.

We wachten op (**'on'**) bepaalde events en voeren dan een functie uit.

Socket.io kan ook callback functies uitvoeren, server kan meteen antwoorden.

Server kan **broadcast**en naar alle verbonden clients.
- Broadcast: alle behalve mezelf
- emit: inclusief mezelf

Socket clients kunnen ook in rooms zitten.
Socket clients kunnen ook private messages sturen naar elkaar.

https://socket.io/docs/v3/emit-cheatsheet/

## Summary
- Wat is MQTT?
- Wat zijn topics & subscriptions?
- Wat zijn de wildcard opties voor MQTT?
- Wat is QoS?
- Wat zijn Websockets?
- Wat zijn de voordelen van Socket.io?