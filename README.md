MQTT, short for Message Queuing Telemetry Transport, is a lightweight messaging protocol ideal for IoT (Internet of Things) and other machine-to-machine (M2M) applications.MQTT primarily uses the TCP/IP protocol. It operates on a publish/subscribe model, meaning devices can publish messages to a topic and others can subscribe to that topic to receive them. This architecture allows for efficient, low-bandwidth communication, making it suitable for resource-constrained devices and unreliable networks.

MQTT typically uses port 1883 for unencrypted connections and 8883 for secure connections using TLS/SSL encryption. Additionally, MQTT can also operate over WebSockets using port 443.
Here's a more detailed breakdown:
Port 1883: This is the standard, default port for unencrypted MQTT communication.
Port 8883: This is the default port for secure MQTT connections using TLS/SSL encryption. This port is registered with IANA for secure MQTT.
Port 443: MQTT can also be used over WebSockets, which typically use port 443.

MQTT is an event-driven protocol also often called real time transport protocol(RTP), which means data shared/transmitted only when an event occurs, like publish or changes in data in case of subscribers. this keeps the machine free and uses resources only when needed. So it is best suited for real time monitoring like iot applications.

Here's a more detailed explanation:

1. Publish/Subscribe Model:
   MQTT uses a publish/subscribe pattern, where devices (clients) act as either publishers or subscribers.
   Publishers: send messages to a specific topic, and the message is then delivered to all subscribers who have subscribed to that topic.
   Subscribers: register their interest in specific topics and receive messages published to those topics.
   This decoupling of publishers and subscribers allows for a flexible and scalable communication system.
2. MQTT Broker:
   (ex: io.adafruit.com is a cloud based broker, we can also set up local brokers like Mosquitto etc)
   A central server, called the MQTT broker, manages the communication between clients.
   It handles routing messages from publishers to the appropriate subscribers based on their subscriptions.
   The broker also acts as a message queue, temporarily storing messages for subscribers who may be offline or temporarily disconnected.
3. Lightweight and Efficient:
   MQTT is designed to be lightweight and efficient, using a minimal amount of bandwidth and resources.
   It's particularly well-suited for devices with limited processing power and battery life, like sensors and actuators.
   The binary nature of MQTT messages further contributes to its efficiency, as it requires less data overhead compared to text-based protocols like HTTP.
4. MQTT in IoT:
   MQTT is widely used in IoT applications for its ability to facilitate communication between various devices, sensors, and cloud platforms.
   It allows for real-time data exchange, enabling smart homes, industrial automation, and other connected systems.
   MQTT's ability to handle large numbers of devices and its scalability make it a popular choice for large-scale IoT deployments.
5. MQTT Versions:
   MQTT 3.1.1 and MQTT 5 are the two main versions of the protocol.
   MQTT 5 introduced enhancements like enhanced security features, support for more transport layers, and increased flexibility in message handling.
   Most commercial MQTT brokers now support MQTT 5, but some IoT-managed cloud services still primarily support MQTT 3.1.1.

   The Publish/Subscribe (Pub/Sub) model. How it Works:

6. Publishers send messages to the broker:
   Publishers don't send messages directly to subscribers; instead, they send them to a specific topic on the broker.
7. Subscribers subscribe to topics:
   Subscribers express interest in receiving messages related to specific topics.
8. The broker routes messages to subscribers:
   The broker receives messages and routes them to all subscribers who have subscribed to the corresponding topic.
9. Subscribers process the messages:
   Subscribers receive and process the messages they are interested in.
   Benefits of the Pub/Sub Model:
   Decoupling:
   Publishers and subscribers are independent of each other, allowing for more flexible and scalable systems.
   Scalability:
   The system can handle a large number of publishers and subscribers without affecting the performance of individual components.
   Asynchronous Communication:
   Publishers don't need to wait for subscribers to receive messages, allowing for more efficient communication.
   Flexibility:
   The system can be easily adapted to different application requirements.

   The Keep Alive mechanism in MQTT ensures the connection’s liveliness and provides a way for the broker to detect if a client becomes unresponsive or disconnected.
   as the broker is a server and cannot initiate request when an event occurs, insted MQTT keeps the connection active when the client(devices eg esp32) requests for connection.
   Keep Alive is a feature of the MQTT protocol that allows an MQTT client to maintain its connection with a broker by sending regular control packets called PINGREQ to the broker. the brocker in return responds with PINGRESP confirming that the connection is active.

   When a client establishes a connection with an MQTT broker, it negotiates a Keep Alive value, which is a time interval expressed in seconds. The client must send a PINGREQ packet to the broker at least once within this interval to indicate its presence and keep the connection alive. Upon receiving a PINGREQ packet, the broker responds with a PINGRESP packet, confirming that the connection is still active and thus makes event driven/real time communication possible.

| Supported Targets | ESP32 | ESP32-C2 | ESP32-C3 | ESP32-C6 | ESP32-H2 | ESP32-S2 | ESP32-S3 |
| ----------------- | ----- | -------- | -------- | -------- | -------- | -------- | -------- |

# ESP-MQTT sample application

(See the README.md file in the upper level 'examples' directory for more information about examples.)

This example connects to the broker URI selected using `idf.py menuconfig` (using mqtt tcp transport) and as a demonstration subscribes/unsubscribes and send a message on certain topic.
(Please note that the public broker is maintained by the community so may not be always available, for details please see this [disclaimer](https://iot.eclipse.org/getting-started/#sandboxes))

Note: If the URI equals `FROM_STDIN` then the broker address is read from stdin upon application startup (used for testing)

It uses ESP-MQTT library which implements mqtt client to connect to mqtt broker.

## How to use example

### Hardware Required

This example can be executed on any ESP32 board, the only required interface is WiFi and connection to internet.

### Configure the project

- Open the project configuration menu (`idf.py menuconfig`)
- Configure Wi-Fi or Ethernet under "Example Connection Configuration" menu. See "Establishing Wi-Fi or Ethernet Connection" section in [examples/protocols/README.md](../../README.md) for more details.

### Build and Flash

Build the project and flash it to the board, then run monitor tool to view serial output:

```
idf.py -p PORT flash monitor
```

(To exit the serial monitor, type `Ctrl-]`.)

See the Getting Started Guide for full steps to configure and use ESP-IDF to build projects.

## Example Output

```
I (3714) event: sta ip: 192.168.0.139, mask: 255.255.255.0, gw: 192.168.0.2
I (3714) system_api: Base MAC address is not set, read default base MAC address from BLK0 of EFUSE
I (3964) MQTT_CLIENT: Sending MQTT CONNECT message, type: 1, id: 0000
I (4164) MQTT_EXAMPLE: MQTT_EVENT_CONNECTED
I (4174) MQTT_EXAMPLE: sent publish successful, msg_id=41464
I (4174) MQTT_EXAMPLE: sent subscribe successful, msg_id=17886
I (4174) MQTT_EXAMPLE: sent subscribe successful, msg_id=42970
I (4184) MQTT_EXAMPLE: sent unsubscribe successful, msg_id=50241
I (4314) MQTT_EXAMPLE: MQTT_EVENT_PUBLISHED, msg_id=41464
I (4484) MQTT_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=17886
I (4484) MQTT_EXAMPLE: sent publish successful, msg_id=0
I (4684) MQTT_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=42970
I (4684) MQTT_EXAMPLE: sent publish successful, msg_id=0
I (4884) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (4884) MQTT_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
I (5194) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (5194) MQTT_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
```
