# Sea & Sahara Comms (SSCHN)
## Project Brief

**Document ID:** SSCHN-DOC-01  
**Version:** 0.1  
**Status:** Draft — Pending Engineering Review  
**Project:** Sea & Sahara Comms — Secure Hybrid Communication Network  
**Target MVP Duration:** Approximately 12 weeks  
**Available Development Time:** Approximately two full working days per week

---

## 1. Executive Summary

Sea & Sahara Comms (SSCHN) is a proposed offline-capable communication system designed for remote marine, desert, and field environments where conventional mobile connectivity or internet access may be unavailable, unreliable, or impractical.

The initial Minimum Viable Product (MVP) will demonstrate short text-message communication between physical ESP32-based nodes using compatible LoRa radio hardware. Messages will be received and processed by local software, stored in a local database, and displayed through a web dashboard. The prototype will also demonstrate an end-to-end SOS alert workflow.

The system will be designed to operate locally without requiring internet connectivity for its core communication and dashboard functionality.

The project will prioritize a working physical prototype, measurable test results, a maintainable software structure, and a clear technical demonstration over feature count.

The proposed architecture and hardware selection remain provisional until reviewed by an experienced electronics/networking engineer.

## 2. Problem Statement

Remote marine operations, desert travel, field maintenance, and other activities outside reliable connectivity coverage may lack a practical way to exchange simple messages and communicate urgent events between nearby team members.

Existing communication options may depend on cellular coverage, satellite subscriptions, specialized equipment, or infrastructure that is not always available or economical for small operators.

SSCHN explores a modular alternative that uses local radio communication for nearby devices, with a locally operated software system for receiving, recording, and displaying messages and alerts.

The initial prototype is intended to validate the technical feasibility of this approach. It does not yet establish commercial readiness, guaranteed communication range, regulatory compliance, or suitability for safety-critical operations.

## 3. Target Users and Operational Scenarios

Potential users include:

- **Fishermen and small marine operators:** Exchanging basic messages between nearby team members or vessels where conventional connectivity is limited.
- **Desert convoys and remote field teams:** Communicating short operational updates between team members.
- **Oil and gas field operations:** Exchanging basic field messages in locations with limited connectivity.
- **Remote maintenance teams:** Reporting status updates and requesting assistance.
- **Emergency and disaster-response teams:** Exploring local message exchange when conventional infrastructure is unavailable.

These are potential application areas, not validated customer segments. The MVP will establish technical feasibility rather than prove market demand.

## 4. Proposed Solution

SSCHN will use low-power long-range radio technology, based on LoRa-compatible transceivers, to exchange small messages between portable electronic nodes.

Each node will use an ESP32 development board and a compatible LoRa radio module, subject to engineering validation. The nodes will implement a simple application-level message protocol for identifying senders, distinguishing message types, and handling basic delivery and duplicate-detection behavior.

A local gateway will receive radio messages and forward valid messages to application software. A local backend and database will manage device information, messages, timestamps, and alert events. A web dashboard will provide a visual interface for monitoring the prototype.

The initial system will use a simple, explicitly defined radio protocol rather than assuming that LoRaWAN or mesh networking is available automatically.

## 5. Product Vision

The long-term vision is a modular communication platform for remote environments that can exchange messages without depending on cellular service or continuous internet connectivity.

Potential future capabilities include:

- Offline text messaging.
- SOS and emergency notifications.
- GPS/GNSS-based location sharing.
- Store-and-forward relaying or multi-hop networking.
- Local gateways and operational dashboards.
- Stronger device authentication and message-integrity protections.
- Optional satellite forwarding for selected critical messages.
- Additional hardware and communication interfaces.

These capabilities represent future development opportunities. They are not commitments for the initial MVP.

## 6. MVP Objectives

The MVP will aim to:

1. Establish a working radio link between two physical nodes.
2. Exchange text messages without internet access.
3. Identify message sources and distinguish ordinary messages from SOS events.
4. Demonstrate message reception and forwarding to local application software.
5. Store messages and device information in a local database.
6. Display devices, messages, and SOS events in a web dashboard.
7. Implement and test a basic message-delivery mechanism, including acknowledgements and bounded retries where supported by the selected design.
8. Implement a practical baseline for message authentication and integrity, subject to hardware and library validation.
9. Measure message-delivery performance under documented test conditions.
10. Produce technical documentation and a repeatable end-to-end demonstration.

## 7. MVP Features

### 7.1 Portable Communication Nodes

- Two physical ESP32-based nodes.
- Compatible LoRa radio modules and correctly matched antennas.
- Unique node identifiers.
- Basic text-message transmission and reception.
- Defined message types, including SOS.
- Message identifiers or sequence information for duplicate detection.
- Basic diagnostics and error reporting.
- Acknowledgements and bounded retries, as supported by the selected protocol.

### 7.2 Gateway

- A compatible radio interface for receiving application-level LoRa packets.
- Packet parsing and basic structural validation.
- Forwarding of valid messages to local application software.
- Diagnostic logging.
- Handling of malformed packets and unavailable application services.

The gateway may initially run on the development laptop. A dedicated Raspberry Pi or other computer will be considered only if justified by the architecture, integration needs, and budget.

### 7.3 Backend and Database

- A local API for gateway integration and dashboard data access.
- Storage of devices, messages, timestamps, and SOS events.
- Basic message and device retrieval.
- Health and diagnostic endpoints.
- Operation without cloud services.

### 7.4 Web Dashboard

- Device list and available last-seen information.
- Message log with sender, message type, and timestamp.
- SOS alert visibility.
- Gateway and application status.
- Location display when actual GPS/GNSS integration is available.
- Clearly labelled simulated location data during software development, if necessary.

### 7.5 Security and Reliability

- Defined message identifiers and duplicate-handling rules.
- Bounded retries and acknowledgement timeouts.
- A practical message-authentication and integrity mechanism.
- Basic replay protection where feasible.
- Secure handling of cryptographic keys and configuration secrets.
- Documented tests for delivery, duplicate handling, gateway disconnection, and malformed messages.

The exact cryptographic implementation and radio parameters require engineering review before finalization.

## 8. Explicitly Excluded Features

The following are excluded from the initial MVP scope:

- Satellite communication hardware and subscriptions.
- Drone-based relays.
- Full mesh networking and dynamic routing.
- Custom PCB design and fabrication.
- Advanced environmental or industrial sensors.
- Solar charging systems.
- Production-grade ruggedization or waterproofing.
- Large-scale cloud infrastructure.
- Multi-user commercial account management.
- Claims of guaranteed message delivery or a guaranteed radio range.
- Deployment as a certified emergency or safety-critical communication system.

A feature may be reconsidered only if the core demonstration is stable, the remaining schedule permits it, and the change is explicitly approved.

## 9. Assumptions and Constraints

### 9.1 Confirmed Project Constraints

- The project is being developed primarily by one person.
- Available development time is approximately two full working days per week.
- The target duration is approximately 12 weeks.
- An electronics/networking engineer is available to review hardware and technical decisions.
- The incubator is expected to assist with obtaining required components.
- The developer has programming experience but is still developing practical embedded-electronics and radio-engineering skills.

### 9.2 Provisional Design Assumptions

- ESP32 development boards will be used for the portable nodes.
- SX1276/RFM95W-class LoRa hardware is a candidate, not a confirmed purchase.
- Direct node-to-node communication will be validated before adding relay functionality.
- A laptop will host the initial gateway and application software wherever practical.
- The backend, database, and dashboard will operate locally.
- GPS/GNSS will be optional for the first physical radio milestone.
- A third node will be considered only if it provides a clear testing or gateway benefit.

### 9.3 Constraints Requiring Validation

- Appropriate LoRa frequency band and applicable Algerian regulations.
- Radio-module compatibility and availability.
- Antenna frequency, connector, and electrical compatibility.
- Transmit power and radio configuration.
- Power-supply requirements and safe portable operation.
- Security-library compatibility with the chosen microcontroller.
- Local hardware prices, procurement lead times, and budget.
- Practical communication range under documented test conditions.

## 10. Proposed System Overview

The provisional system consists of four layers.

**Layer 1 — Portable Radio Nodes**

ESP32-based devices exchange application-level messages using compatible LoRa transceivers and antennas. Each node constructs, transmits, receives, and parses packets.

**Layer 2 — Radio Gateway**

A gateway receives packets through a compatible LoRa interface, validates their structure, and forwards messages to the local application. Its final hardware arrangement remains subject to review.

**Layer 3 — Local Application Services**

A backend API processes incoming messages, manages device and alert records, and stores data in a local database.

**Layer 4 — Web Dashboard**

A browser-based dashboard displays available device information, message history, SOS events, and system status.

The core node-to-node radio link must function independently of internet connectivity. Internet access, if available, must not be a prerequisite for the local MVP workflow.

**Future extensions:** Satellite forwarding and store-and-forward relaying will remain separate, deferred capabilities.

## 11. Expected Demonstration

The final demonstration should show the following sequence:

1. Power on two physical communication nodes.
2. Confirm that each node has a distinct identifier.
3. Send a text message from Node A to Node B without internet access.
4. Demonstrate reception and, where implemented, an acknowledgement from the receiving node.
5. Send a message that can be received by the gateway.
6. Display the received message in the local application and store it in the database.
7. Open the dashboard and inspect the recorded message.
8. Trigger an SOS event and demonstrate its transmission, reception, storage, and display.
9. Demonstrate relevant error handling, such as a malformed packet or temporary gateway disconnection.
10. Present documented measurements from repeatable message-delivery tests.

If GPS hardware is not integrated, the dashboard must clearly distinguish simulated coordinates from actual device location.

The demonstration must not imply that a simulated function has been implemented in physical hardware.

## 12. Success Criteria

The MVP will be considered demonstrable when:

- Two physical nodes exchange messages over the selected LoRa link without internet access.
- The receiver can identify the sender and parse valid messages.
- The gateway can forward received messages to the local backend.
- The backend stores messages and associated metadata.
- The dashboard displays stored messages and SOS events.
- The end-to-end SOS workflow can be reproduced.
- Implemented acknowledgement, retry, duplicate-handling, and security behaviors pass their documented tests.
- Message-delivery results are measured and recorded under specified conditions.
- The core workflow continues to operate on the local machine or local network without cloud dependencies.
- The documentation describes the final configuration, limitations, and steps needed to reproduce the demonstration.

Numerical performance targets will be established after the hardware and radio configuration are selected and reviewed. No measured results or guaranteed range are claimed at this stage.

## 13. Main Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Hardware incompatibility | Obtain engineer approval before procurement; verify interfaces, frequency, and electrical requirements. |
| Procurement delays | Prioritize the smallest viable hardware order and use documented software simulations only for parallel application development. |
| Radio range below expectations | Measure performance under controlled conditions; document antenna placement and radio settings. |
| Radio regulations or unsuitable frequency | Confirm the applicable requirements with authoritative sources and the engineer before transmitting. |
| Power or battery safety issues | Begin with USB-powered bench testing and validate portable power arrangements before use. |
| Security implementation complexity | Select established libraries and keep the initial security design narrow and reviewable. |
| Gateway integration problems | Separate the radio interface from the application backend and test each boundary independently. |
| Scope expansion | Defer satellite, drone, mesh, and advanced hardware features until the core workflow works. |
| Limited development time | Prioritize the physical radio link, gateway integration, message logging, and SOS demonstration. |
| Misleading test results | Record test conditions, attempts, successful deliveries, duplicates, and observed limitations. |

## 14. Roles and Responsibilities

### Project Developer

Responsible for:

- Project coordination and technical documentation.
- Firmware development with guidance where needed.
- Gateway software and integration.
- Backend API and database.
- Web dashboard.
- Software testing and system integration.
- Repository maintenance and demonstration preparation.

### Electronics/Networking Engineer

Expected to review and advise on:

- Radio architecture and regulatory considerations.
- Board and module compatibility.
- Antennas and radio configuration.
- Electrical interfaces and power requirements.
- Battery safety and hardware assembly.
- Gateway hardware choices.
- Feasibility of the security and reliability design.
- Procurement decisions and major technical risks.

### Incubator

Expected to assist with:

- Reviewing the prototype plan.
- Approving or arranging hardware procurement.
- Identifying available equipment and local sourcing options.
- Supporting the planned prototype demonstration.

These responsibilities are proposed working arrangements and may be adjusted with the people involved.

## 15. Questions Requiring Engineer Approval

Before finalizing the hardware procurement request, confirm:

1. Which frequency band is appropriate and lawful for the intended use in Algeria?
2. Which exact ESP32 board and LoRa module combination should be purchased?
3. Are the selected radio modules electrically compatible with the chosen boards?
4. Which antennas and connectors are required?
5. Which radio parameters and transmit-power limits should be used for initial testing?
6. Is the proposed direct-link and gateway topology sufficient?
7. Can the laptop host the gateway initially, or is dedicated hardware required?
8. What power arrangement is appropriate for bench testing and later portable operation?
9. Should GPS/GNSS be included in the initial procurement?
10. Which established cryptographic implementation is suitable for the chosen hardware?
11. Are the proposed packet size, acknowledgements, retries, and duplicate-handling strategy practical?
12. What is the minimum hardware order needed to prove the concept?
13. Which components or test equipment can be borrowed or replaced with existing equipment?
14. Which risks could materially affect the 12-week target?

## 16. Technical Terminology

- **MVP (Minimum Viable Product):** The smallest working prototype that demonstrates the project's essential value and technical feasibility.
- **ESP32:** A family of microcontrollers used to run embedded software and interface with external hardware.
- **LoRa:** A long-range, low-power radio modulation technology suitable for transmitting relatively small amounts of data.
- **LoRaWAN:** A networking protocol and architecture built around LoRa radio technology. It is distinct from a custom application-level LoRa protocol.
- **Node:** An individual communication device in the system.
- **Gateway:** A component that bridges the radio communication layer and local application software.
- **Packet:** A structured unit of data transmitted over a communication link.
- **Acknowledgement (ACK):** A response indicating that a particular message or packet was received according to the protocol's defined rules.
- **Retry:** A controlled retransmission attempt following a timeout or another defined failure condition.
- **Duplicate detection:** Identifying repeated messages so that retransmissions do not unintentionally create repeated application actions.
- **Authentication:** Verifying that a message or device possesses the credentials required by the protocol.
- **Message integrity:** Detecting unauthorized modification of a message.
- **Replay protection:** Detecting or rejecting previously captured messages that are retransmitted maliciously or unintentionally.
- **GPS/GNSS:** Satellite-based positioning technologies used to obtain device location.
- **Mesh networking:** A network in which nodes can forward traffic for other nodes according to defined forwarding or routing rules.
- **Store-and-forward:** Receiving a message, retaining it temporarily, and forwarding it later when the next communication opportunity is available.
- **Backend:** The application services that process data, expose APIs, and coordinate database operations.
- **API (Application Programming Interface):** A defined interface through which software components exchange data and request operations.

## 17. Document Status and Next Steps

This document establishes the proposed scope and direction of the SSCHN MVP. It is not a final hardware specification, radio-compliance assessment, or safety certification.

The next steps are:

1. Review this brief and resolve any scope ambiguities.
2. Prepare the system architecture diagram.
3. Develop testable functional and non-functional requirements.
4. Prepare the provisional hardware bill of materials.
5. Obtain engineer feedback before committing to hardware procurement.
6. Finalize the software design and implementation roadmap.
7. Begin development with the two-node physical LoRa communication milestone.

**Document status:** Draft — Pending Engineering Review.