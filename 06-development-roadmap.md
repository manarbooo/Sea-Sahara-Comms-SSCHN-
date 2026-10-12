# 06 — Development Roadmap

**Project:** Sea & Sahara Comms (SSCHN)  
**Version:** 0.2  
**Target Duration:** 12 weeks  
**Available Time:** Approximately two full working days per week

## 1. Objective

Build and validate the SSCHN MVP incrementally, beginning with physical LoRa communication and progressing toward a locally integrated messaging and SOS demonstration.

**Priority:** Working hardware first, functional software second, integration and testing throughout. Satellite communication, drones, and mesh networking remain outside the MVP.

## 2. Development Phases

| Phase | Timeline | Main Deliverables |
|---|---|---|
| 1. Preparation | Weeks 1–2 | Engineer-approved hardware plan, development environment, repository structure, initial firmware and packet design |
| 2. Radio Link | Weeks 3–4 | Two physical nodes exchanging text messages in both directions |
| 3. Gateway | Weeks 5–6 | Gateway radio reception, USB serial communication, laptop gateway software |
| 4. Backend and Database | Weeks 7–8 | Local API, persistent message storage, gateway integration |
| 5. Dashboard and SOS | Weeks 9–10 | Message history, SOS display, device activity, end-to-end workflow |
| 6. Testing and Demonstration | Weeks 11–12 | Reliability and security checks, performance measurements, documentation, final demonstration |

These are planning estimates, not guaranteed deadlines. Hardware procurement, radio debugging, and engineering feedback may require adjustments.

## 3. Phase Details

### Phase 1 — Preparation (Weeks 1–2)

- Review the project brief, architecture, and requirements with the engineer.
- Confirm the exact boards, LoRa frequency configuration, antennas, power requirements, and procurement list.
- Set up the development environment and firmware libraries.
- Establish a repository structure for firmware, gateway software, backend, frontend, and tests.
- Define the initial packet format and message types.

**Milestone:** Hardware and development decisions are sufficiently validated to begin implementation.

### Phase 2 — Physical Radio Link (Weeks 3–4)

- Bring up each board and verify USB serial communication.
- Assign unique device IDs.
- Implement packet creation, transmission, reception, and validation.
- Test Node A → Node B and Node B → Node A.
- Add basic message identifiers and diagnostics.
- Implement acknowledgements and bounded retries if time and design permit.

**Milestone:** Two physical nodes exchange valid messages without internet access.

Do not proceed to complex application integration until this basic link works.

### Phase 3 — Gateway Integration (Weeks 5–6)

- Configure the third radio board as the gateway interface, if approved.
- Establish USB serial communication between the gateway board and laptop.
- Implement a gateway program that reads, parses, and validates received packets.
- Test gateway reception independently from direct node-to-node delivery.
- Log malformed packets and connection failures.

**Milestone:** A supported radio packet can travel from a node through the gateway interface to the laptop.

### Phase 4 — Backend and Database (Weeks 7–8)

- Implement a local backend API.
- Create database records for messages and devices.
- Store received message content, identifiers, types, and reception timestamps.
- Connect gateway software to the backend.
- Implement message-history and device-status endpoints.
- Test persistence after a backend restart.

**Milestone:** Messages received through the gateway are stored and retrievable locally.

### Phase 5 — Dashboard and SOS (Weeks 9–10)

- Build the browser-based dashboard.
- Display messages with sender, type, and reception time.
- Distinguish SOS events from ordinary messages.
- Display available device activity and system status.
- Implement and test the SOS workflow across the physical communication path and gateway.
- Use simulated data only where needed for interface development, clearly labelling it.

**Milestone:** A physical message can be received through the gateway, stored, and displayed in the dashboard; the SOS workflow is demonstrable.

### Phase 6 — Testing and Final Demonstration (Weeks 11–12)

- Test bidirectional communication and gateway reception.
- Test malformed packets, duplicates, retries, and disconnections where implemented.
- Review message authentication, integrity, and key handling.
- Measure packet delivery ratio under documented conditions.
- Record test setup, radio configuration, distance, and limitations.
- Fix critical integration problems.
- Finalize setup instructions, architecture, and demonstration steps.

**Milestone:** A repeatable end-to-end demonstration and a documented test report.

## 4. Technical Priorities

Follow this order when deciding what to implement:

1. **Essential:** Physical two-node communication.
2. **Essential:** Gateway radio reception and laptop integration.
3. **Essential:** Local backend, database, and message history.
4. **Essential:** SOS message workflow.
5. **Essential:** Basic validation, error handling, and measured performance.
6. **Important:** Acknowledgements, retries, and duplicate detection.
7. **Important:** Practical message authentication and integrity.
8. **Optional:** GNSS location, batteries, enclosures, and interface refinements.

Optional features must not delay the core demonstration.

## 5. Testing and Measurements

Record at least:

- Number of packets transmitted.
- Number of valid packets received.
- Packet delivery ratio.
- Test distance and environment.
- Radio configuration and antenna placement.
- Whether results refer to direct node-to-node delivery or gateway reception.
- Observed failures, duplicates, and communication delays.

**Packet Delivery Ratio (PDR):**

PDR (%) = (Valid packets received ÷ Packets transmitted) × 100

Calculate the ratio separately for direct node-to-node communication and gateway reception.

## 6. Development Rules

- Test each hardware and software boundary independently before integration.
- Keep the core system local and independent of internet access.
- Use simulated packets to develop software in parallel, but never treat simulation as proof of radio performance.
- Commit working changes to Git regularly.
- Document hardware configuration and important technical decisions.
- Record known limitations rather than hiding incomplete features.
- Avoid adding new features until the current milestone is demonstrated.

## 7. Main Risks to the Schedule

| Risk | Response |
|---|---|
| Hardware arrives late | Develop packet parsing, backend, and dashboard with clearly labelled simulated data. |
| Radio communication is unreliable | Focus on basic board setup, antenna compatibility, configuration, and controlled tests. |
| Gateway does not receive node traffic | Diagnose radio settings and gateway listening behavior separately from direct communication. |
| Security takes longer than expected | Use established libraries and consult the engineer; do not invent cryptographic primitives. |
| Integration exceeds available time | Reduce optional features and preserve the essential end-to-end workflow. |

## 8. Definition of Done

The MVP is ready for demonstration when two physical nodes exchange text messages, the gateway receives and forwards supported packets, the local backend stores them, and the dashboard displays messages and SOS events without requiring internet access.

Implemented reliability and security features must be tested and documented. Communication performance must be measured, and limitations must be stated clearly.

**Final deliverable:** A working prototype, source code, setup instructions, architecture documentation, and a reproducible demonstration with recorded test results.