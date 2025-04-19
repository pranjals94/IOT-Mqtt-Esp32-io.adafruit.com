How push notification service works

In a private network, you don’t have access to public cloud services like Firebase Cloud Messaging (FCM) or Apple Push Notification Service (APNs). So, we build our own local push notification server.

How Push Notification Works (in Private Network)
Client Devices (like mobile apps, browsers, or embedded devices) register with your server.

Your Push Server stores device info (like IP or a socket session) in a database.

When an event happens, the server sends a message to the device over a persistent connection (e.g., WebSocket, MQTT, or HTTP Long Polling).

The device receives it and displays the notification.


Non-persistent connection:   Client sends request → Server responds → Connection closes (e.g., normal HTTP)
Persistent connection: Client connects → Connection stays open → Server can send messages anytime

Why Persistent Connections Matter (especially for Push Notifications)
Because:

The server needs to push data to the client whenever it wants — not wait for the client to ask.

A persistent connection keeps the channel open so the server can send updates in real-time.

examples:
Protocol		Description

WebSocket		Two-way, full-duplex communication over a single TCP connection. Great for web & mobile apps.
MQTT			Lightweight protocol used in IoT for persistent connections. Efficient and low bandwidth.
Socket.IO		JS library that adds real-time, event-based communication (built on WebSocket + fallback).
gRPC (streaming)	Used in microservices for persistent data streams.
HTTP/2 with keep-alive	Modern HTTP with persistent connection support.