# App Overview

## What is Apex Datalogger?

This is a telemetry acquisition tool made for Assetto Corsa that captures captures high-frequency car physics data in real time.

It works as an offline-first telemetry tool capturing over 180+ channels of data with precise timestamps for post-session analysis while also oferring built-in live telemetry streaming.

The app runs in the background while the simulator is running. All data processes are controlled by two independent modes: LOG and TX. With both LOG and TX modes disabled, no channels are read, no data is processed, and no data is transmitted. **The app remains fully idle in this state** with no impact on performance. 

> **Note:** Activation of the telemetry acquisition occurs only when at least one of the two modes is turned on.

Apex runs two app windows inside Assetto Corsa: **Apex Settings** and **Apex HUD** which can be closed at any time without affecting LOG or TX features. You can bind custom buttons to toggle LOG or TX modes via **Extended Controls app**.

## Modes

### LOG Mode

LOG mode is the local data logging function. When active, it works as a full onboard motorsports datalogger: it records car telemetry directly
to your PC's file system, organized by stint.

- **Stint driven**: To start logging, the logger detects when the car begins a stint (leaving pits, session start, or race green flag). When the stint ends (manually returning to pits, session end, race finish or manual cancellation), the logger exports a `log_TIMESTAMP_DRIVERNAME_TRACK_CAR.json` with the metadata of the stint.
- **Stint logging**: Telemetry data is continously written into a stint CSV file exported as `log_TIMESTAMP_DRIVERNAME_TRACK_CAR.csv`with all the information obtained in that stint.
- **Independent**: LOG mode can record without TX mode active.

All files are written to the `laps/` folder within the app folder. You can access them directly from the in-game app settings.

### TX Mode

TX mode is the real-time telemetry transmitter. It streams live channel data via UDP to a specific IP and port, enabling external applications such as analysis tools.

- **UDP stream**: TX mode broadcasts telemetry UDP packets to a configurable IP address and port.
- **Send-and-forget**: The protocol used is **unidirectional** with no handshake or acknowledgment. If no receiver is actively listening, packets are silently dropped.
- **Independent**: TX mode does not require LOG mode to be active.

> **Important**: Both **LOG** and **TX** modes use the exact same channel groups. Disabling a channel group in settings stops both modes recording and streaming
> for that group.