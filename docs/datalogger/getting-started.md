# Getting Started

## App Overview

Apex datalogger is a telemetry acquisition tool made for AC that captures captures high-frequency car physics data.

The app runs in the background while the simulator is running. All data processes are controlled by two independent modes: LOG and TX. 
With both LOG and TX modes disabled, no channels are read, no data is processed, and no data is transmitted. The app remains fully idle in this state with no impact on performance. 

> **Note:** Activation of the datalogger occurs only when at least one of the two modes is turned on.

Both app windows **Apex Settings** and **Apex HUD** can be closed at any time without affecting LOG or TX. Toggling ON and OFF either
mode doesn't require the UI windows open. See the Keybindings section below to map buttons for LOG and TX through the **Extended Controls app**.

### LOG Mode

LOG mode is the local data logging function. When active, it works as a full onboard motorsports datalogger: it records car telemetry directly
to your PC's file system, organized by lap.

- **Stint driven**: To start logging, the logger detects when the car begins a stint (leaving pits, session start, or race green flag). When the stint ends (manually returning to pits, session end, race finish or manual cancellation), the logger exports a `log_175961_drivername.json` with the metadata of the stint.
- **Per-lap logging**: Telemetry data is continously written into lap segments. Each time the car crosses the start/finish line, the lap is saved
as `lap_175961_1_drivername.csv` with all the information obtained of that specific lap.
- **Independent**: LOG mode can record without TX mode active.

All files are written to the `laps/` folder within the app folder.

### TX Mode

TX mode is the real-time telemetry transmitter. It streams live channel data via UDP to a specific IP and port, enabling external applications 
such as analysis tools.

- **UDP stream**: TX mode broadcasts telemetry UDP packets to a configurable IP address and port.
- **Send-and-forget**: The protocol used is **unidirectional** with no handshake or acknowledgment. If no receiver is actively listening, packets are
silently dropped.
- **Independent**: TX mode does not require LOG mode to be active.

> **Important**: Both **LOG** and **TX** modes use the exact same channel groups. Disabling a channel group in settings stops both modes recording and streaming
> for that group.

## Initial Setup

To get the most out of Apex Datalogger, make sure **Enable Python apps** is enabled in Content Manager.

> **Note:** This enables the Python buffer required to extract additional data for suspension.

1. Go to **Settings**
2. Go to **Assetto Corsa** sub section
3. Navigate to **Python Apps**
4. Check the **Enable Python apps** checkbox

<img src="../assets/04enablepy.png" alt="lua-folder">

When in session two apps should be accesible from the apps sidebar:

<p align=center>
<img src="../assets/05apps.png" alt="lua-folder">
</p>

1. **Apex**: This is the **Apex Settings** app, used for settings and configurations related to LOG and TX modes for telemetry and data.
2. **Apex Hud**: A small compact HUD to show the current status related to LOG and TX modes.

## Apex Settings

<p align=center>
<img src="../assets/06app.png" alt="logging-tab">
</p>

### Logging Tab

1. Navigation bar
2. Toggle LOG mode button:
3. Toggle TX mode button
4. LOG mode indicator
5. Clear Console button
6. Console

### Data Tab

<p align=center>
<img src="../assets/07app.png" alt="data-tab">
</p>

1. CSP Data information
2. Python Buffer app status (`active` or `inactive`)
3. Logged laps folder shortcut button
4. Extra Track and Car information

<p align=center>
<img src="../assets/lapsfolder.png" alt="laps-folder" width=460>
</p>
<p align=center> <em>Logged laps folder example</em> </p>

### Settings Tab

<p align=center>
<img src="../assets/08app.png" alt="settings-tab">
</p>

1. Driver management
2. App global settings JSON file shortcut button
3. Channel Groups checkboxes
4. Custom Channels
5. LOG mode
6. TX mode settings

## Apex HUD

<p align=center>
<img src="../assets/10apphud.png" alt="hud">
</p>
<p align=center> <em>Completely inactive app status (both indicators turned OFF, app on idle)</em> </p>

1. TX mode indicator
2. LOG mode indicator

### TX Indicator

<table>
  <thead>
    <tr>
      <th>TX Mode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <img src="../assets/11apphud.png" alt="tx-off" width="370">
      </td>
      <td>
        When TX mode is inactive, the dot indicator will be off. No data is being collected or processed.
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/12tx.gif" alt="tx-on" width="370">
      </td>
      <td>
        When TX mode is active, the dot indicator will blink. Data is being collected and sent via UDP.
      </td>
    </tr>
  </tbody>
</table>

### LOG Indicator

<table>
  <thead>
    <tr>
      <th>LOG Mode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <img src="../assets/11apphud.png" alt="log-off" width="370">
      </td>
      <td>
        When LOG mode is inactive, the dot indicator will be off. No data is being collected or processed.
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/13apphud.png" alt="log-waiting" width="370">
      </td>
      <td>
        When LOG mode is active (but not logging yet), the dot indicator will turn yellow. No data is being collected or processed. This is the standby state of the LOG mode.
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/14apphud.png" alt="log-on" width="370">
      </td>
      <td>
        When LOG mode is running (logging) the dot indicator will turn green. Data is being collected and processed. 
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/12log.gif" alt="log-saving" width="370">
      </td>
      <td>
        The LOG indicator dot will blink for two seconds when saving a lap.
      </td>
    </tr>
  </tbody>
</table>

## Assign Custom Buttons

Thanks to the capabilities of **External Controls app**, you can assign custom buttons to enable or disable LOG and TX modes without the need
of having the **Apex Settings** window open.

<p align=center>
<img src="../assets/15ext.png" alt="hud">
</p>

Open the **Extended Controls** window, and navigate to **Apps** (1) > **Apex** (2) > **Shortcuts** (3). And simply assign the button for toggle LOG mode and TX mode.

<p align=center>
<img src="../assets/16ext.png" alt="hud">
</p>
