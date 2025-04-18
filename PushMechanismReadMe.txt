connections are often kept alive for push mechanisms like server sent events(sse)and web sockets to enable Realtime two communication.

push Mechanism: first the client requests to the server then token may be received by the client for the push notification communication and after that the connection is keept alive.
which enables the server to push notifications/messages to the client when an event occurs on the server. This is the most common method for "push notifications" in laptop or mobiles.


"Keep-alive" refers to a network connection that remains open between a client and a server for multiple requests,

Understanding TCP Keep-Alive
TCP keep-alive is a mechanism that enables two devices to maintain an open connection even when there is no data transmission. It sends periodic messages (keep-alive packets) between the devices to ensure that the connection remains active. If either device fails to receive a keep-alive packet, it will assume that the other device is no longer available, and the connection will be terminated.

TCP keep-alive is especially useful in situations where a device may go offline or become unresponsive for extended periods. Without keep-alive, the connection would eventually timeout, and the devices would need to re-establish the connection from scratch. This would result in additional latency and potential data loss.

An Overview of TCP Connection Maintenance
TCP connections require active maintenance to remain open. Without maintenance, connections may become unresponsive or time out, resulting in a disruption of service. There are two primary techniques that devices use to maintain TCP connections: TCP keep-alive and TCP retransmission.

TCP retransmission is a technique used to recover from lost, corrupted, or delayed packets. When a device fails to receive an expected packet, it will request that the packet be retransmitted. This allows for reliable data transmission over the internet, where packet loss and network congestion are common.

TCP keep-alive, on the other hand, is used to keep the connection active even when there is no data to transmit. It sends periodic messages to ensure that the connection remains open and available for data transmission.

TCP Keep-Alive Parameters
TCP keep-alive requires several parameters to function properly. These parameters include the keep-alive timer, keep-alive interval, and keep-alive probe count.

Keep-Alive Timer
The keep-alive timer is the amount of time a device will wait before sending a keep-alive packet. If no data is transmitted during this time, the device will send a keep-alive packet to ensure that the connection remains active.

Keep-Alive Interval
The keep-alive interval is the time between keep-alive packets. This interval should be long enough to prevent excessive network traffic but short enough to ensure that the connection remains active.

Keep-Alive Probe Count
The keep-alive probe count is the number of keep-alive packets that a device will send before assuming that the connection is no longer available. If the device fails to receive a response after sending the specified number of keep-alive packets, it will assume that the connection has timed out and terminate the connection.

The Anatomy of Keep-Alive Packets and Timers
Keep-alive packets are simple messages that devices use to maintain an open connection. They consist of a header and a payload. The header contains various fields, including the source and destination IP addresses and port numbers, as well as flags that indicate whether the packet is a keep-alive packet.

The payload of the keep-alive packet is generally empty or contains a small amount of data. This data is used to verify that the connection is still active and to prevent the connection from timing out.

The keep-alive timer and interval are essential parameters that determine how frequently keep-alive packets are sent. If these parameters are set too low, it can result in excessive network traffic, while setting them too high can result in the connection timing out.