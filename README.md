# LabVIEW UDP Communication App

## Overview

This application was developed in the **LabVIEW** environment and utilizes the **UDP communication protocol** for bidirectional data transmission between a server and a client. It is designed to demonstrate real-time communication using structured messages transmitted over a local network.

## Features

- Bidirectional UDP communication between server and client
- Real-time data transmission and reception
- Structured message format with:
  - **Timestamp**
  - **Array of numerical values** (from external signal generator)
  - **Boolean flag** for transmission termination
- Graphical user interface with:
  - Timestamp display
  - Waveform graph
  - LED indicator for end of transmission
- Remote shutdown of the server via a secondary UDP channel

---


## Communication Details

### Server (ServerUDP.vi)

- Sends UDP packets to `localhost` on port `61555`
- Uses port `61550` as sender
- Message sent every **1 second**
- Message contains:
  - **Current timestamp**
  - **Generated array** from `Generator.vi`
  - **Boolean**: `False` normally, becomes `True` after 1 minute to signal end
- Cluster is flattened to string before sending
- Terminates automatically after sending the "end" message

### Client (ClientUDP.vi)

- Listens on UDP port `61555`
- Receives string, unflattens it into a cluster
- Displays:
  - Timestamp
  - Signal on waveform graph
  - End-of-transmission LED
- Terminates on:
  - Receiving `True` in end-of-transmission field
  - Timeout (30 seconds of inactivity)

### Extended Functionality

- Implements a second communication loop:
  - Client sends a shutdown command to server
  - Uses ports `61556` (client sender) and `61551` (server listener)
  - Allows **remote termination** of the server by client

## Usage

1. Open the LabVIEW project.
2. Run `ServerUDP.vi`.
3. Run `ClientUDP.vi`.
4. Observe the data exchange.
5. Wait 1 minute for auto shutdown **or** use the client to trigger remote termination.

## Requirements

- **LabVIEW 2020 or newer**
- UDP enabled and allowed in system firewall (localhost only)








