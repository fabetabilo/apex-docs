# Getting Started

## App Windows

When in session two apps should be accesible through the apps sidebar:

<p align=center>
<img src="../assets/apps-sidebar.png" alt="lua-folder">
</p>

## Apex HUD

A small compact HUD to show the current status related to LOG and TX modes.

<p align=center>
<img src="../assets/apphud.png" alt="hud">
</p>
<p align="center">
  <sub><i>Logger on idle, both indicators turned OFF, no data is being collected</i></sub>
</p>

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
        <img src="../assets/11apphud.png" alt="log-off" width="600">
      </td>
      <td>
        When LOG mode is inactive, the dot indicator will be off. No data is being collected or processed.
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/13apphud.png" alt="log-waiting" width="600">
      </td>
      <td>
        When LOG mode is active (but not logging), the dot indicator will turn yellow. No data is being collected or processed. The app is waiting for the stint to start.
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/14apphud.png" alt="log-on" width="600">
      </td>
      <td>
        When LOG mode is running (logging) the dot indicator will turn green. Data is being collected and processed. 
      </td>
    </tr>
    <tr>
      <td>
        <img src="../assets/12log.gif" alt="log-saving" width="600">
      </td>
      <td>
        The LOG indicator dot will blink for two seconds when crossing the start-line.
      </td>
    </tr>
  </tbody>
</table>

## Apex Settings

This is the settings app, used for configurations related to LOG and TX modes for telemetry and data.

### Logging

<p align=center>
<img src="../assets/logging-tab.png" alt="logging-tab">
</p>

1. Toggle LOG mode button
2. Toggle TX mode button
3. LOG status indicator
4. Open laps folder button
5. Clear Console button
6. Logger console

### Data

<p align=center>
<img src="../assets/data-tab.png" alt="data-tab">
</p>

1. CSP Aeromap and encrypted aero detection
2. Python Buffer app status (`active` or `inactive`)
3. Track id information
4. Extra car information

### Settings

<p align=center>
<img src="../assets/settings-tab.png" alt="settings-tab">
</p>

1. Driver management
2. LOG logging mode
3. TX mode settings for target IP and Port
4. Channels groups selection
5. Variable channels selection
6. Sampling rate selection for fast groups; `Input`, `GPS`, `Tire Dynamics`, `G-force`, `Suspension`
7. Settings file shortcut button

### About

<p align=center>
<img src="../assets/about-tab.png" alt="about-tab">
</p>

1. Apex Datalogger version
2. Custom Shaders Patch version
3. Link button to app releases
4. Official documentation link button

## Map Custom Buttons

Thanks to the capabilities of **External Controls** app, you can assign custom buttons to enable or disable LOG and TX modes without the need of having the **Apex Settings** window open.

<p align=center>
<img src="../assets/15ext.png" alt="hud">
</p>

Open the **Extended Controls** window, and navigate to **Apps** > **Apex** > **Shortcuts**. And simply assign the button for toggle LOG mode and TX mode.

<p align=center>
<img src="../assets/ext-controls.png" alt="extended-controls">
</p>

1. Custom toggle LOG button
2. Custom toggle TX button