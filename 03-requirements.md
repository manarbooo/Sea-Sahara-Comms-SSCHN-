# 03 — System Requirements

**Project:** Sea & Sahara Comms (SSCHN)  
**Version:** 0.3

## 1. Objective

Define the functional and technical requirements for an offline communication prototype using ESP32-based LoRa nodes, a separate gateway interface, and a locally hosted application.

## 2. Scope

**Included:** Two physical nodes, bidirectional text messaging, packet handling, gateway reception, local backend and database, dashboard, SOS messages, and performance testing.

**Excluded:** Satellite communication, drones, full mesh networking, cellular connectivity, cloud dependency, custom PCBs, and advanced sensors.

## 3. Functional Requirements

| ID | Requirement |
|---|---|
| SYS-01 | Each node must have a unique device ID. |
| SYS-02 | Nodes must exchange text messages bidirectionally over LoRa. |
| SYS-03 | Users must be able to send messages through a serial terminal or simple interface. |
| SYS-04 | Packets must include a protocol version, packet ID, source, destination, message type, and payload. |
| SYS-05 | The system must distinguish ordinary messages from SOS messages. |
| SYS-06 | Invalid or malformed packets must be rejected safely. |
| SYS-07 | The firmware should support acknowledgements, retries, and duplicate detection. |

## 4. Gateway Requirements

| ID | Requirement |
|---|---|
| GTW-01 | A separate, compatible LoRa radio interface must receive packets; a laptop alone cannot receive LoRa directly. |
| GTW-02 | The gateway interface must transfer received data to the laptop, provisionally over USB serial. |
| GTW-03 | Gateway software must parse, validate, and forward received packets to the backend. |
| GTW-04 | The gateway must provide basic connection and error diagnostics. |

**Important:** Direct node-to-node transmission does not guarantee that the gateway will receive the same packet. Gateway reception must be configured and tested separately.

## 5. Backend and Dashboard

| ID | Requirement |
|---|---|
| APP-01 | The backend must expose a local API for the dashboard. |
| APP-02 | The database must store received messages, device IDs, message types, and timestamps. |
| APP-03 | The dashboard must display message history and clearly identify SOS messages. |
| APP-04 | The system should display each device's last observed activity. |
| APP-05 | Message history must remain available after a backend restart. |
| APP-06 | Core functionality must work without internet access. |

## 6. SOS and Security

- Users must be able to generate an SOS message from a node.
- The receiving node and/or gateway dashboard must identify and display the SOS message according to the implemented communication path.
- The prototype must not claim delivery to emergency services unless that capability is actually implemented.
- Document the security design, including device identity, message integrity, confidentiality, and key management.
- Authenticated encryption should be implemented if feasible within the MVP schedule.
- Secrets and encryption keys must not be committed to the repository.
- Communication failures must not be reported as successful delivery.

## 7. Hardware Dependencies

The engineer must confirm the following before purchase or final implementation:

- Exact ESP32/LoRa board model and revision.
- Supported frequency and compliant radio configuration for Algeria.
- Compatible antennas, connectors, and power requirements.
- Firmware libraries and gateway compatibility.
- Whether additional USB-to-serial hardware or other interface components are required.

## 8. Verification and Testing

| Test | Expected Result |
|---|---|
| Bidirectional radio test | Both nodes successfully exchange valid messages. |
| Packet validation | Malformed packets are rejected. |
| Gateway reception | The gateway receives and transfers supported packets to the laptop. |
| Backend integration | Valid gateway packets are stored in the database. |
| Dashboard integration | Messages and SOS events appear correctly. |
| Offline operation | Core communication and local application work without internet. |
| Restart test | Stored message history survives a backend restart. |
| Failure handling | Disconnections and invalid data are handled without false success reports. |
| Performance test | Packet delivery and communication delays are measured under documented conditions. |

### Packet Delivery Ratio

**Packet Delivery Ratio (PDR) (%) = (Valid packets received ÷ Packets transmitted) × 100**

Measure direct node-to-node delivery and gateway reception separately. Record the number of packets transmitted, valid packets received, test duration, distance, and test conditions.

## 9. Completion Criteria

The MVP is complete when:

- Two physical nodes exchange text messages in both directions.
- A separate gateway receives packets and transfers them to the laptop.
- The local backend, database, and dashboard operate without internet access.
- SOS messages are identifiable along the implemented communication path.
- Basic error handling and performance tests are completed.
- Setup instructions, architecture, and test results are documented.

**Next action:** Validate the hardware and radio configuration with the engineer, then demonstrate a basic two-node LoRa link before developing the complete application.