# Sea & Sahara Comms (SSCHN)
## Project Brief

**Document ID:** SSCHN-DOC-01  
**Version:** 0.2  
**Status:** Draft — Pending Engineering Review  
**Target MVP Duration:** Approximately 12 weeks  
**Available Development Time:** Approximately two full working days per week

## 1. Executive Summary

Sea & Sahara Comms (SSCHN) is an offline-capable communication system designed for remote marine, desert, and field environments where cellular coverage and internet access may be unavailable or unreliable.

The Minimum Viable Product (MVP) will demonstrate bidirectional text messaging between two physical ESP32-based devices using compatible LoRa radio hardware. A separate radio gateway will receive supported packets and transfer them to software running on a laptop. A local backend and database will process and store messages, while a web dashboard will display message history, device activity, and SOS alerts.

The core workflow will operate without internet access. The prototype will focus on proving technical feasibility, measuring communication performance, and demonstrating a reproducible end-to-end system.

Hardware choices, radio configuration, and security implementation remain subject to engineering review.

## 2. Problem and Proposed Solution

Teams working at sea, in deserts, or at remote industrial sites may need to exchange short messages when conventional communication infrastructure is unavailable.

SSCHN explores a modular alternative based on local radio communication and locally operated software. It aims to provide a practical way to exchange basic messages, record operational events, and communicate SOS alerts without depending on continuous internet connectivity.

The MVP will validate the technical approach. It will not establish commercial readiness, guaranteed radio range, or suitability for safety-critical operations.

## 3. Target Users

Potential application areas include:

- **Marine operations:** Fishermen and small vessels operating where conventional connectivity is limited.
- **Desert and remote teams:** Convoys, field personnel, and teams working across isolated areas.
- **Industrial operations:** Oil and gas personnel and remote maintenance teams.
- **Emergency response:** Exploring local communication when conventional infrastructure is disrupted.

These are proposed use cases; customer demand and commercial viability require separate validation.

## 4. How the System Works

The proposed system has four main layers.

### 4.1 Communication Nodes

Each portable node uses a microcontroller, a compatible LoRa radio, and an antenna.

When a user sends a message, the node packages the information into a structured data packet and transmits it over the radio link. Another node receives the packet, checks its structure, identifies the sender and message type, and presents the message to the user.

The nodes are intended to communicate directly without internet access.

### 4.2 Radio Gateway

A separate LoRa-capable board receives radio packets and transfers the received data to the laptop, provisionally over USB serial.

The laptop does not receive LoRa signals by itself: it needs the gateway's radio hardware. The gateway must also be configured to receive the relevant transmissions; it is not guaranteed to hear every packet exchanged directly between two nodes.

Gateway software on the laptop parses and validates the incoming data before forwarding it to the local application.

### 4.3 Local Backend and Database

The backend provides an API through which the gateway software submits received messages and the dashboard retrieves stored information.

The database records messages, device identifiers, timestamps, and SOS events. These services run locally, without requiring a cloud server.

### 4.4 Web Dashboard

A browser-based dashboard displays recorded messages, sender information, message types, SOS events, and available device activity.

Actual location information will only be shown if suitable positioning hardware is integrated. Simulated coordinates used during development must be clearly labelled.

### End-to-end message flow

1. A user enters a message on Node A.
2. Node A transmits the packet over LoRa.
3. Node B receives and validates the packet.
4. If the gateway also receives the transmission, it forwards the data to the laptop.
5. Gateway software validates the data and submits it to the backend.
6. The backend stores the message in the database.
7. The dashboard retrieves and displays the recorded message.

Direct node-to-node delivery and gateway reception are separate behaviors and must be tested independently.

## 5. MVP Scope

### Included

- Two physical ESP32-based LoRa nodes with unique identifiers.
- Bidirectional text messaging over a direct radio link.
- A defined packet format with message types and packet identifiers.
- Basic packet validation and duplicate detection.
- A separate LoRa gateway interface connected to a laptop.
- Local gateway software, backend API, and database.
- A browser-based dashboard with message history and SOS visibility.
- A basic SOS transmission and reception workflow.
- Acknowledgements and bounded retries, subject to the selected design.
- A practical message-authentication and integrity mechanism, subject to hardware and library validation.
- Documented communication and failure-handling tests.

### Excluded

- Satellite communication and subscriptions.
- Drone-based relays.
- Full mesh networking and dynamic routing.
- Custom PCB design.
- Advanced environmental or industrial sensors.
- Solar charging and production-grade ruggedization.
- Cloud infrastructure and commercial account management.
- Certified emergency communications or guarantees of message delivery and range.

Future features will only be reconsidered after the core MVP works reliably.

## 6. Technical Approach

The initial implementation will use a simple application-level packet protocol over LoRa rather than assuming that LoRaWAN or mesh networking is automatically available.

A packet is expected to contain:

- Protocol version.
- Packet identifier.
- Source and destination device IDs.
- Message type, such as `TEXT` or `SOS`.
- Message payload.
- Optional timestamp, depending on the availability of a reliable time source.

The implementation should support acknowledgements, bounded retransmissions, and duplicate detection where feasible. Security should use established cryptographic libraries appropriate to the selected hardware, with keys handled securely.

The exact packet encoding, payload limits, radio settings, and cryptographic implementation must be validated during development.

## 7. Hardware and Design Assumptions

The following are provisional choices, not confirmed purchases:

- ESP32 development boards for the communication nodes.
- Compatible LoRa radio hardware; SX1276/RFM95W-class hardware has been considered.
- A third compatible radio board for the gateway, if validated as the simplest practical arrangement.
- A laptop hosting the gateway software, backend, database, and dashboard.
- USB-powered bench testing before introducing batteries or portable enclosures.
- Optional GPS/GNSS integration after the basic radio link works.

Before procurement, the engineer must verify the exact board models, radio compatibility, appropriate and lawful frequency configuration in Algeria, antennas, power requirements, and software-library support.

## 8. Demonstration and Success Criteria

The final demonstration should show that:

1. Two physical nodes can exchange messages in both directions without internet access.
2. The receiver identifies the sender and parses valid packets.
3. The gateway can receive supported packets and transfer them to the laptop.
4. The backend stores received messages and associated metadata.
5. The dashboard displays message history and SOS events.
6. The SOS workflow can be reproduced end to end along the implemented communication path.
7. Implemented reliability and security behaviors pass documented tests.
8. Communication performance is measured under recorded test conditions.
9. The local system remains usable without cloud services.

Tests should record transmitted and successfully received packets, test duration, distance, radio configuration, antenna placement, and relevant environmental conditions.

No numerical performance target or guaranteed communication range is claimed before the hardware is selected and tested.

## 9. Schedule, Resources, and Constraints

The target is approximately 12 weeks, with around two full working days available per week. Development is primarily undertaken by one person with programming experience and developing practical embedded-electronics and radio-engineering skills.

An electronics/networking engineer is available for technical review, and the incubator is expected to assist with hardware procurement.

The schedule should prioritize the following milestones:

1. Validate hardware choices and establish serial communication.
2. Demonstrate bidirectional messaging between two physical nodes.
3. Configure and test the gateway radio interface.
4. Build the local backend, database, and dashboard.
5. Integrate and demonstrate SOS messaging.
6. Test reliability, security, and communication performance.
7. Finalize documentation and the repeatable demonstration.

Software components may be developed using simulated packets while hardware procurement is pending, but simulations must not be presented as proof of physical radio functionality.

## 10. Main Risks and Mitigation

| Risk | Mitigation |
|---|---|
| Incompatible hardware | Obtain engineering approval before purchasing. |
| Radio configuration or regulatory issues | Confirm applicable Algerian requirements and suitable settings before transmitting. |
| Limited radio performance | Measure under controlled conditions and document the limitations. |
| Procurement delays | Order only essential hardware first and develop independent software components in parallel. |
| Security complexity | Use established libraries and validate the design with the engineer. |
| Gateway integration difficulties | Test radio reception, serial transfer, and backend integration separately. |
| Scope expansion | Defer satellite, drone, mesh, and advanced hardware features. |
| Limited development time | Prioritize the physical radio link, gateway, local message history, and SOS demonstration. |

## 11. Engineer Review Questions

Before finalizing procurement and implementation, confirm:

1. Which LoRa frequency band and configuration are lawful and appropriate in Algeria?
2. Which exact ESP32 board and LoRa module should be selected?
3. Which antennas, connectors, and power arrangements are required?
4. Is the proposed direct-link and separate-gateway topology suitable?
5. Can the laptop host the gateway and application software, or is additional computing hardware necessary?
6. Which radio settings and payload limits should be used?
7. Which cryptographic library and security approach are practical for the selected board?
8. Are acknowledgements, retries, and duplicate detection feasible within the planned schedule?
9. Is GPS/GNSS necessary for the initial demonstration?
10. What is the minimum hardware order required to validate the concept?

## 12. Technical Terminology

| Term | Meaning in SSCHN |
|---|---|
| **MVP** | Minimum Viable Product: the smallest working prototype that demonstrates the essential functionality. |
| **ESP32** | A family of microcontrollers that can run embedded software and interface with external hardware. |
| **LoRa** | A low-power, long-range radio modulation technology suited to transmitting relatively small amounts of data. |
| **LoRaWAN** | A networking protocol and architecture built on LoRa radio technology; it is different from a custom packet protocol. |
| **Node** | A communication device that sends and/or receives messages. |
| **Gateway** | The radio-connected component that bridges LoRa communication and the laptop's application software. |
| **Packet** | A structured unit of data transmitted over a communication link. |
| **ACK (Acknowledgement)** | A protocol response indicating that a particular packet or message was received according to defined rules. |
| **Retry** | A controlled retransmission after a timeout or another defined failure condition. |
| **Duplicate detection** | Identifying repeated packets so that retransmissions do not unintentionally trigger repeated actions. |
| **Authentication** | Verifying that a device or message has valid credentials or proof of origin. |
| **Message integrity** | Detecting unauthorized changes to message contents. |
| **Replay protection** | Detecting or rejecting previously captured messages that are retransmitted. |
| **GPS/GNSS** | Satellite-based positioning technologies used to determine a device's location. |
| **Mesh networking** | A network in which nodes can forward traffic for other nodes according to defined forwarding or routing rules. |
| **Store-and-forward** | Temporarily retaining a message and forwarding it when another communication opportunity becomes available. |
| **Backend** | Application services that process data, expose APIs, and manage database operations. |
| **API** | Application Programming Interface: a defined way for software components to exchange data and request operations. |
| **Delivery ratio** | The percentage of transmitted packets successfully received according to the test's defined success criteria. |

## 13. Next Steps

1. Finalize the architecture and requirements documents.
2. Review the proposed hardware and radio configuration with the engineer.
3. Confirm the minimum hardware order with the incubator.
4. Begin with the two-node physical LoRa link.
5. Add gateway integration, local application services, and the dashboard incrementally.
6. Document the final configuration, test results, and limitations.

**Document status:** Draft — Pending Engineering Review.