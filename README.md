# Smart India Hackathon Workshop

## Date: 18/09/2026

## Register Number: 212223220118

## Name: THIRUMURUGAN R

## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations

## Problem Description
Railway stations are complex environments with platforms, ticket counters, restrooms, food courts, waiting areas, lifts, escalators and multiple entrances and exits. Passengers, especially first-time visitors, senior citizens and passengers with disabilities, may find it difficult to locate facilities and reach the correct platform quickly.

The proposed system provides an indoor navigation solution with detailed station maps, step-by-step directions, accessibility-aware routing, voice guidance, digital kiosks and regularly updated station information.

## Problem Creator's Organization
Ministry of Railway

# Idea

### RailNav360 — Smart Railway Station Indoor Navigation

RailNav360 is a smart indoor navigation system designed to help passengers find facilities and reach their destinations inside railway stations.

The system provides a digital station map containing platforms, ticket counters, restrooms, waiting halls, food courts, lifts, escalators, entrances and exits. Instead of depending completely on GPS, the system uses a station navigation graph with QR/NFC checkpoints to improve indoor positioning.

### Key Features

- Indoor digital maps for railway stations.
- Step-by-step navigation to platforms and facilities.
- A* based shortest-path navigation.
- Accessibility-aware routes for wheelchair users and passengers with limited mobility.
- QR/NFC checkpoints for indoor location assistance.
- Voice-guided navigation.
- Multilingual interface.
- Offline map support when internet connectivity is weak.
- Digital kiosks with touch-screen navigation.
- Kiosk-to-mobile route transfer using a QR code.
- Admin dashboard for updating maps, facilities and temporary closures.
- Dynamic route recalculation when a path is unavailable.

### What Makes the Idea Different

The solution combines Indoor Maps + Navigation Graph + QR/NFC Checkpoints + Accessibility Routing + Voice Guidance + Digital Kiosks in one system. This reduces dependence on GPS and allows station-specific navigation information to be updated by administrators.

# Proposed Solution / Architecture Diagram

## 1. System Architecture

~~~mermaid
flowchart TD
    P[Passenger] --> M[Mobile Application]
    P --> K[Digital Kiosk]
    M --> API[Backend REST API]
    K --> API
    API --> MAP[Station Map Service]
    API --> NAV[Navigation Engine]
    API --> POS[Indoor Position Service]
    API --> VOICE[Voice & Language Service]
    API --> STATUS[Station Status Service]
    NAV --> GRAPH[Station Navigation Graph]
    NAV --> ACCESS[Accessibility Rules]
    POS --> QR[QR/NFC Checkpoints]
    API --> DB[(Station Database)]
    API --> CACHE[Offline Map Cache]
    A[Station Administrator] --> ADMIN[Admin Dashboard]
    ADMIN --> API
    API --> RAIL[Railway Information Services]
~~~

## 2. Navigation Process

~~~mermaid
flowchart LR
    A[Select Destination] --> B[Identify Current Location]
    B --> C[Load Station Map]
    C --> D[Apply Accessibility Preferences]
    D --> E[Calculate Route using A*]
    E --> F[Show Step-by-Step Directions]
    F --> G[Voice Guidance]
    G --> H{Path Available?}
    H -- Yes --> I[Continue Navigation]
    H -- No --> J[Recalculate Route]
    J --> I
~~~

### Navigation Algorithm

The station is represented as a graph:

- Nodes: platforms, facilities, entrances, exits, lifts, escalators and checkpoints.
- Edges: walkable paths between nodes.
- Weights: distance, estimated walking time and accessibility restrictions.

The system can use the A* algorithm to calculate an efficient route.

A* formula: f(n) = g(n) + h(n)

Where:
- g(n) = cost from the starting point to node n.
- h(n) = estimated cost from node n to the destination.
- f(n) = total estimated route cost.

For accessibility mode, paths containing stairs can be removed or given a high cost, while lifts and ramps are preferred.

## 3. Indoor Positioning

QR/NFC checkpoints are placed at important locations such as entrances, platforms, lifts and major junctions. When a passenger scans a checkpoint, the application can update the passenger's current position on the station map.

This approach is useful because GPS accuracy can be limited inside large buildings.

## 4. Kiosk-to-Mobile Navigation

A passenger can select a destination at a station kiosk. The kiosk displays the route and generates a QR code. Scanning the QR code on the mobile application transfers the selected destination and route information to the passenger's phone.

# Use Cases

## Main Actors

- Passenger
- Station Administrator
- Digital Kiosk
- Railway Information System

## Use Case Table

| Use Case | Actor | Description |
|---|---|---|
| View Station Map | Passenger | Displays the indoor station map. |
| Search Facility | Passenger | Searches for platforms, restrooms, food courts and other facilities. |
| Find Platform | Passenger | Provides directions to the selected platform. |
| Get Route | Passenger | Calculates a route from the current location to the destination. |
| Accessibility Mode | Passenger | Generates routes suitable for wheelchair and low-mobility users. |
| Scan QR/NFC | Passenger | Updates indoor position using a checkpoint. |
| Voice Navigation | Passenger | Provides spoken step-by-step directions. |
| Change Language | Passenger | Allows the user to select a supported language. |
| Offline Navigation | Passenger | Uses cached station maps when connectivity is weak. |
| Kiosk Navigation | Passenger | Gets directions through a station kiosk. |
| Update Station Map | Administrator | Adds or modifies station facilities and paths. |
| Temporary Closure | Administrator | Marks blocked or unavailable paths/facilities. |
| Sync Railway Data | Railway System | Provides updated railway or station information. |

## Use Case Diagram

~~~mermaid
flowchart LR
    P[Passenger]
    A[Station Administrator]
    K[Digital Kiosk]
    R[Railway Information System]
    P --> U1[View Station Map]
    P --> U2[Search Facility]
    P --> U3[Get Route]
    P --> U4[Accessibility Mode]
    P --> U5[Scan QR/NFC]
    P --> U6[Voice Navigation]
    P --> U7[Change Language]
    P --> U8[Offline Navigation]
    K --> U9[Kiosk Navigation]
    A --> U10[Update Station Map]
    A --> U11[Manage Closures]
    R --> U12[Sync Railway Data]
~~~

## Example User Scenario

A passenger enters a large railway station and needs to reach Platform 5.

1. The passenger opens RailNav360.
2. The application identifies the entrance/checkpoint location.
3. The passenger selects Platform 5.
4. The system checks accessibility preferences.
5. A* calculates a suitable route.
6. The application displays the route on the station map.
7. Voice guidance provides step-by-step instructions.
8. If the passenger reaches a QR/NFC checkpoint, the position is updated.
9. If a path becomes unavailable, the route is recalculated.

# Technology Stack

| Layer | Technology / Approach |
|---|---|
| Web Frontend | React, HTML, CSS, JavaScript/TypeScript |
| Mobile Application | React Native / Android |
| Backend | Node.js, Express.js, REST API |
| Database | PostgreSQL or Firebase |
| Navigation | Graph-based routing, A* algorithm |
| Indoor Maps | SVG/JSON based custom station maps |
| Positioning | QR/NFC checkpoints |
| Voice | Text-to-Speech |
| Kiosk | React-based touch-screen interface |
| Admin Dashboard | React web application |
| Development | VS Code, Git, GitHub |
| API Testing | Postman |
| Future Enhancements | BLE, AR, computer vision and railway APIs |

# Dependencies

## Frontend

~~~bash
npm install react react-dom
npm install react-router-dom
~~~

## Backend

~~~bash
npm install express cors dotenv
~~~

## Optional Dependencies

- QR code scanner/generator library.
- Text-to-Speech support.
- PostgreSQL client or Firebase SDK.
- React Native navigation and camera packages.
- Mapping/visualization libraries if required.

## Software Requirements

- Node.js and npm.
- Git.
- GitHub account.
- VS Code or another code editor.
- Modern web browser.
- Android Studio for Android development.

## Hardware for Kiosk Deployment

- Touch-screen display.
- Mini PC or suitable computer.
- QR scanner/camera.
- Network connection.
- Optional speaker for voice guidance.

# Advantages

- Easy indoor navigation for passengers.
- Reduces confusion in large stations.
- Supports accessibility requirements.
- QR/NFC improves indoor positioning.
- Provides voice guidance.
- Supports both mobile users and kiosk users.
- Allows administrators to update station information.
- Can recalculate routes when paths are blocked.

# Future Enhancements

- BLE beacon-based positioning.
- AR-based walking directions.
- Real-time crowd-density information.
- Integration with live railway APIs.
- AI-based route recommendations.
- Computer-vision assisted indoor positioning.
- Emergency route guidance.
- More Indian-language voice support.

# Project Structure

~~~text
SIH-1710/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── use-cases.md
│   └── evaluation.md
├── frontend/
├── mobile/
├── backend/
├── kiosk/
└── admin/
~~~

# Implementation Roadmap

1. Design the station map.
2. Create station nodes, paths and facilities.
3. Implement the navigation graph.
4. Implement A* route calculation.
5. Add accessibility filtering.
6. Add QR/NFC checkpoints.
7. Develop mobile navigation screens.
8. Develop digital kiosk interface.
9. Develop administrator dashboard.
10. Add voice and multilingual support.
11. Add offline map caching.
12. Test the system with different passenger scenarios.

# Testing Plan

The system should be tested for:

- Correct route generation.
- Accessibility route correctness.
- QR/NFC checkpoint detection.
- Voice instruction accuracy.
- Offline map loading.
- Kiosk-to-mobile transfer.
- Route recalculation after a path closure.
- Map update synchronization.
- Different screen sizes and devices.

# Academic Integrity

This README describes the proposed RailNav360 concept for the SIH 1710 workshop. The implementation, diagrams and documentation should be developed and maintained by the project team. Any external libraries, datasets or railway services used during implementation should be properly acknowledged.
