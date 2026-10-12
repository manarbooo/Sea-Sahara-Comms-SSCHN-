# 05 — Software Design

**Project:** Sea & Sahara Comms (SSCHN)  
**Version:** 0.1

## 1. Overview

The software consists of four components: node firmware, gateway software, a local backend, and a web dashboard. Communication between nodes uses LoRa; the gateway connects the radio system to the laptop application.

## 2. Components

### 2.1 Node Firmware — `firmware/esp32-node/`

Runs on each ESP32-based LoRa board.

Responsibilities:
- Assign a unique device ID.
- Accept text input through USB serial or a simple interface.
- Build and transmit LoRa packets.
- Receive and validate incoming packets.
- Support acknowledgements, retries, and duplicate detection where implemented.
- Identify SOS messages.
- Output status and error information for debugging.

### 2.2 Gateway Software — `gateway/`

Runs on the laptop and communicates with a separate LoRa-capable gateway board.

Responsibilities:
- Read packet data from the gateway board over USB serial.
- Parse and validate received data.
- Reject malformed packets and identify duplicates.
- Forward valid messages to the backend through a local API.
- Log connection status and errors.

**Important:** The laptop does not receive LoRa signals by itself. The gateway board handles radio reception and passes data to the laptop.

### 2.3 Backend — `backend/`

Runs locally on the laptop.

Responsibilities:
- Provide a local HTTP API.
- Receive validated messages from the gateway software.
- Store messages and metadata in a database.
- Provide message history and device activity to the dashboard.
- Handle invalid requests and report errors.

A lightweight backend and database should be used initially to minimize setup and development time.

### 2.4 Dashboard — `frontend/`

A local web interface accessible through a browser.

Responsibilities:
- Display received messages and timestamps.
- Distinguish SOS messages visually.
- Show device IDs and last observed activity when available.
- Display basic system or gateway status.
- Allow users to review message history.

The dashboard communicates with the backend, not directly with the LoRa radio.

## 3. Message Structure

Each packet should use a consistent format.

| Field | Purpose |
|---|---|
| `version` | Protocol version |
| `packet_id` | Unique packet identifier |
| `source_id` | Sender device ID |
| `destination_id` | Intended recipient |
| `message_type` | For example, `TEXT` or `SOS` |
| `payload` | Message content |
| `timestamp` | Optional timestamp, depending on available time source |

The final encoding and maximum payload size must be confirmed against the selected radio configuration. A timestamp must not be assumed accurate if the device has no reliable clock.

## 4. Data Flow

### Sending a message

1. The user enters a message on Node A.
2. Node A constructs a packet and transmits it over LoRa.
3. Node B receives and validates the packet.
4. Node B displays or outputs the message.
5. If acknowledgements are implemented, Node B may send an acknowledgement to Node A.

### Receiving a message through the gateway

1. A node transmits a packet over LoRa.
2. The gateway board receives the packet when its radio configuration and listening state permit.
3. The gateway board sends the received data to the laptop over USB serial.
4. Gateway software parses and validates the data.
5. The software forwards valid messages to the local backend.
6. The backend stores the message in the database.
7. The dashboard retrieves and displays the message.

Direct node-to-node communication and gateway reception must be tested separately.

## 5. Local API

Initial endpoint proposal:

| Method | Endpoint | Purpose |
|---|---|---|
| `POST` | `/api/messages` | Submit a received message from gateway software |
| `GET` | `/api/messages` | Retrieve message history |
| `GET` | `/api/devices` | Retrieve known devices and last observed activity |
| `GET` | `/api/health` | Check backend availability |

The endpoint names are provisional and may be adjusted during implementation.

## 6. Database

The initial database should contain two logical records.

**Messages**
- Internal record ID
- Packet ID
- Source and destination IDs
- Message type
- Payload
- Reception timestamp
- Gateway or validation status, where useful

**Devices**
- Device ID
- Display name, if configured
- Last observed activity

Use the reception timestamp for events recorded by the laptop. Store device-generated timestamps separately if they are later supported and trustworthy.

## 7. Error Handling and Security

- Reject malformed packets and invalid API requests.
- Log serial disconnections, parsing errors, and backend failures.
- Avoid displaying a message as successfully delivered without appropriate confirmation.
- Keep secrets and cryptographic keys out of source control.
- Add authenticated encryption only after basic radio communication and packet handling work.
- Clearly distinguish received messages from simulated or test data.

## 8. Implementation Order

1. Establish serial communication with one board.
2. Implement packet creation and parsing.
3. Demonstrate bidirectional LoRa messaging between two nodes.
4. Configure the third board as the gateway radio interface.
5. Implement laptop serial reading and packet forwarding.
6. Build the backend and database.
7. Build the dashboard and SOS display.
8. Integrate components and test failures, persistence, and radio performance.



**Design principle:** Build and test each layer independently before integrating the complete system.