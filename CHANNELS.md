## Channels

> Document aligned with version `0.2.6` of the logger.

Reference for every channel Apex Datalogger records. Values are written raw, exactly as CSP reports them, with no unit conversion.

### Sampling rates

| Rate | Groups |
|---|---|
| 1 Hz | `session`, `car_info` |
| 10 Hz | `tires`, `dyn`, `ext_elec`, `aero`, `sim_info` |
| Selectable: 30, 50, 60, 100 or 120 Hz | `input`, `gps`, `tires_dyn`, `gforce`, `susp` |

CSP updates car data once per rendered frame, so the real rate of the fast groups is capped by the game FPS. `effectiveRates` in the JSON shows what was actually recorded.

### Conventions

- **Wheels:** wheel suffixes are `fl`, `fr`, `rl`, `rr`, which map to CSP wheel indices 0, 1, 2 and 3.
- **Unit marks:**
  - No mark: the unit is documented in the CSP SDK.
  - `*`: inferred from Assetto Corsa conventions and checked against recorded ranges.
  - `?`: unverified.
- **Unit names:**
  - `0–1` is a ratio.
  - `flag` is `0` / `1` (boolean)
  - `index` is a setting or enum code.
  - `—` means unitless.

### Channels

### `session` (1 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `airtemp` | `SIM.ambientTemperature` | Ambient air temperature | °C* |
| `airdens` | `CPHYS.airDensity` | Air density, affected by slipstream | kg/m³* |
| `roadtemp` | `SIM.roadTemperature` | Road temperature, can vary in shadows if the CSP option is enabled | °C* |
| `roadgrip` | `SIM.roadGrip` | Track grip | 0–1 |
| `winddir` | `SIM.windDirectionDeg` | Wind direction in world space, track heading included | deg |
| `windspeed` | `SIM.windSpeedKmh` | Wind speed | km/h |
| `raceflagtype` | `SIM.raceFlagType` | Flag shown to the driver (`ac.FlagType`) | index |
| `weatherType` | `SIM.weatherType` | Weather type (`ac.WeatherType`) | index |


### `car_info` (1 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `lastsectortime` | `CAR.previousSectorTime`, or the last entry of `CAR.lastSplits` while in the first sector | Time of the previous sector | ms |
| `fuellevel` | `CAR.fuel` | Remaining fuel | l |
| `brakebias` | `CAR.brakeBias` | Brake bias, front share | 0–1* |
| `invalidlap` | `CAR.isLapValid`, inverted | `1` when the current lap is invalid | flag |
| `ebsetting` | `CAR.currentEngineBrakeSetting` | Engine brake setting | index |
| `tiregripfl` | `CAR.wheels[0].tyreWear` | Tyre wear, 0 = new (front left) | 0–1 |
| `tiregripfr` | `CAR.wheels[1].tyreWear` | Tyre wear, 0 = new (front right) | 0–1 |
| `tiregriprl` | `CAR.wheels[2].tyreWear` | Tyre wear, 0 = new (rear left) | 0–1 |
| `tiregriprr` | `CAR.wheels[3].tyreWear` | Tyre wear, 0 = new (rear right) | 0–1 |
| `virtualkmfl` | `CAR.wheels[0].tyreVirtualKM` | Virtual tyre distance; resets on tyre change, and its rate depends on tyre usage (front left) | km |
| `virtualkmfr` | `CAR.wheels[1].tyreVirtualKM` | Virtual tyre distance; resets on tyre change, and its rate depends on tyre usage (front right) | km |
| `virtualkmrl` | `CAR.wheels[2].tyreVirtualKM` | Virtual tyre distance; resets on tyre change, and its rate depends on tyre usage (rear left) | km |
| `virtualkmrr` | `CAR.wheels[3].tyreVirtualKM` | Virtual tyre distance; resets on tyre change, and its rate depends on tyre usage (rear right) | km |
| `damagefront` | `CAR.damage[0]` | Front damage, as collision speed | km/h |
| `damageright` | `CAR.damage[3]` | Right damage, as collision speed | km/h |
| `damagerear` | `CAR.damage[1]` | Rear damage, as collision speed | km/h |
| `damageleft` | `CAR.damage[2]` | Left damage, as collision speed | km/h |
| `tyresCompound` | `CAR.compoundIndex` | Selected compound, an index into `tyresAvail` in the JSON | index |
| `racePosition` | `CAR.racePosition` | Race position, 1 = first | — |
| `engineLifeLeft` | `CAR.engineLifeLeft` | Engine life: 1000 when new, breaks at 0 | — |
| `gearboxDamage` | `CAR.gearboxDamage` | Gearbox damage: 0 when new, 1 when broken | 0–1 |
| `oilTemperature` | `CAR.oilTemperature` | Oil temperature | °C* |
| `waterTemperature` | `CAR.waterTemperature` | Water temperature, an approximation by original AC | °C |
| `absMode` | `CAR.absMode` | ABS setting, 0 = off | index |
| `tcMode` | `CAR.tractionControlMode` | Traction control setting, 0 = off | index |
| `tc2Mode` | `CAR.tractionControl2` | Second traction control setting | index* |
| `fuelMap` | `CAR.fuelMap` | Fuel map preset | index |
| `relplankwear` | `CAR.maxRelativePlankWear` | Highest relative plank wear, 0 if not available | 0–1 |

### `tires` (10 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `tirepressfl` | `CAR.wheels[0].tyrePressure` | Dynamic tyre pressure (front left) | psi* |
| `tirepressfr` | `CAR.wheels[1].tyrePressure` | Dynamic tyre pressure (front right) | psi* |
| `tirepressrl` | `CAR.wheels[2].tyrePressure` | Dynamic tyre pressure (rear left) | psi* |
| `tirepressrr` | `CAR.wheels[3].tyrePressure` | Dynamic tyre pressure (rear right) | psi* |
| `tiresurfdirtfl` | `CAR.wheels[0].surfaceDirt` | Dirt coefficient of the surface below the wheel (front left) | — |
| `tiresurfdirtfr` | `CAR.wheels[1].surfaceDirt` | Dirt coefficient of the surface below the wheel (front right) | — |
| `tiresurfdirtrl` | `CAR.wheels[2].surfaceDirt` | Dirt coefficient of the surface below the wheel (rear left) | — |
| `tiresurfdirtrr` | `CAR.wheels[3].surfaceDirt` | Dirt coefficient of the surface below the wheel (rear right) | — |
| `tiretmpcorefl` | `CAR.wheels[0].tyreCoreTemperature` | Tyre core temperature (front left) | °C |
| `tiretmpcorefr` | `CAR.wheels[1].tyreCoreTemperature` | Tyre core temperature (front right) | °C |
| `tiretmpcorerl` | `CAR.wheels[2].tyreCoreTemperature` | Tyre core temperature (rear left) | °C |
| `tiretmpcorerr` | `CAR.wheels[3].tyreCoreTemperature` | Tyre core temperature (rear right) | °C |
| `tiretmpinnerfl` | `CAR.wheels[0].tyreOutsideTemperature` | Inner tread temperature, relative to the car (front left) | °C |
| `tiretmpinnerfr` | `CAR.wheels[1].tyreInsideTemperature` | Inner tread temperature, relative to the car (front right) | °C |
| `tiretmpinnerrl` | `CAR.wheels[2].tyreOutsideTemperature` | Inner tread temperature, relative to the car (rear left) | °C |
| `tiretmpinnerrr` | `CAR.wheels[3].tyreInsideTemperature` | Inner tread temperature, relative to the car (rear right) | °C |
| `tiretmpmiddlefl` | `CAR.wheels[0].tyreMiddleTemperature` | Middle tread temperature (front left) | °C |
| `tiretmpmiddlefr` | `CAR.wheels[1].tyreMiddleTemperature` | Middle tread temperature (front right) | °C |
| `tiretmpmiddlerl` | `CAR.wheels[2].tyreMiddleTemperature` | Middle tread temperature (rear left) | °C |
| `tiretmpmiddlerr` | `CAR.wheels[3].tyreMiddleTemperature` | Middle tread temperature (rear right) | °C |
| `tiretmpouterfl` | `CAR.wheels[0].tyreInsideTemperature` | Outer tread temperature, relative to the car (front left) | °C |
| `tiretmpouterfr` | `CAR.wheels[1].tyreOutsideTemperature` | Outer tread temperature, relative to the car (front right) | °C |
| `tiretmpouterrl` | `CAR.wheels[2].tyreInsideTemperature` | Outer tread temperature, relative to the car (rear left) | °C |
| `tiretmpouterrr` | `CAR.wheels[3].tyreOutsideTemperature` | Outer tread temperature, relative to the car (rear right) | °C |
| `tyreGrainfl` | `CAR.wheels[0].tyreGrain` | Tyre graining level (front left) | —? |
| `tyreGrainfr` | `CAR.wheels[1].tyreGrain` | Tyre graining level (front right) | —? |
| `tyreGrainrl` | `CAR.wheels[2].tyreGrain` | Tyre graining level (rear left) | —? |
| `tyreGrainrr` | `CAR.wheels[3].tyreGrain` | Tyre graining level (rear right) | —? |
| `tyreBlisterfl` | `CAR.wheels[0].tyreBlister` | Tyre blistering level (front left) | —? |
| `tyreBlisterfr` | `CAR.wheels[1].tyreBlister` | Tyre blistering level (front right) | —? |
| `tyreBlisterrl` | `CAR.wheels[2].tyreBlister` | Tyre blistering level (rear left) | —? |
| `tyreBlisterrr` | `CAR.wheels[3].tyreBlister` | Tyre blistering level (rear right) | —? |
| `braketempfl` | `CAR.wheels[0].discTemperature` | Brake disc temperature (front left) | °C* |
| `braketempfr` | `CAR.wheels[1].discTemperature` | Brake disc temperature (front right) | °C* |
| `braketemprl` | `CAR.wheels[2].discTemperature` | Brake disc temperature (rear left) | °C* |
| `braketemprr` | `CAR.wheels[3].discTemperature` | Brake disc temperature (rear right) | °C* |

### `dyn` (10 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `numtiresout` | `CAR.wheelsOutside` | Wheels outside the allowed track area | count |
| `drivetrainTorque` | `CAR.drivetrainTorque` | Drivetrain torque | Nm* |
| `drivetrainPower` | `CAR.drivetrainPower` | Drivetrain power; matches torque × engine speed expressed in hp | hp* |
| `drivetrainspeed` | `CAR.drivetrainSpeed` | Speed delivered to the wheels; matches the angular speed of the driven wheels | rad/s* |

### `ext_elec` (10 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `drsavail` | `CAR.drsAvailable` | DRS available | flag |
| `drsact` | `CAR.drsActive` | DRS active | flag |
| `erscharging` | `CAR.mguhChargingBatteries` | MGU-H charging the battery | flag |
| `kersdeployed` | `CAR.kersCurrentKJ` | KERS / ERS energy used in the current lap | kJ* |
| `kersinput` | `CAR.kersInput` | KERS deploy input | 0–1* |
| `kerscharge` | `CAR.kersCharge` | Battery charge | 0–1* |

### `aero` (10 Hz)

| Channel | Source | Description | Unit |
|---|---|---|---|
| `aerodrag` | Aero module | Aerodynamic drag force | N* |
| `aeroDownforceFront` | Aero module | Front downforce | N* |
| `aeroDownforceRear` | Aero module | Rear downforce | N* |

The aero module (`src/utils/aero.lua`) picks a source per car and updates at most every 50 ms:

| Car | Source |
|---|---|
| CSP aeromap | The `apex` Python app (`ac.ext_getDrag`, `ac.ext_getDownforce`) |
| Encrypted, with the Python app | Total downforce from the Python app, split 45% front / 55% rear (estimate) |
| Kunos wings | Sum of the wing `CL` / `CD` × 0.5·ρ·v², with the front/rear balance from wing positions |
| No Python app, or no wings | 0 |

### `sim_info` (10 Hz)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `ffbPure` | `CAR.ffbPure` | Force feedback before post-processing | —? |
| `ffbFinal` | `CAR.ffbFinal` | Force feedback sent to the wheel | —? |
| `fps` | `SIM.fps` | Frames per second; caps the real rate of the fast groups | fps |
| `physicsLate` | `SIM.physicsLate` | Late physics steps | count? |
| `cpuTime` | `SIM.cpuTime` | CPU time | ms? |

### `input` (selectable rate)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `clutch` | `CAR.clutch` | Clutch travel | 0–1 |
| `absactive` | `CAR.absInAction` | ABS acting | flag |
| `tcactive` | `CAR.tractionControlInAction` | Traction control acting | flag |
| `speed` | `CAR.speedKmh` | Car speed | km/h |
| `posnorm` | `CAR.splinePosition` | Position along the lap: 0 at the start line, 1 at the finish line | 0–1 |
| `laptime` | `CAR.lapTimeMs` | Current lap time | ms |
| `drivenInRace` | `CAR.drivenInRace` | Distance driven; resets every lap in practice and qualifying, accumulates in races | m |
| `lapcount` | `CAR.lapCount` | Completed laps in the session, invalid laps included | count |
| `throttle` | `CAR.gas` | Throttle | 0–1 |
| `brake` | `CAR.brake` | Brake | 0–1 |
| `handbrake` | `CAR.handbrake` | Handbrake | 0–1 |
| `steerAngle` | `CAR.steer` | Steering wheel angle | deg |
| `steerTorque` | `CAR.steerTorque` | Steering torque | ? |
| `gear` | `CAR.gear` | Gear: 0 = neutral, −1 = reverse | index |
| `rpm` | `CAR.rpm` | Engine speed | rpm |
| `brakeTorqueFL` | `CPHYS.wheels[0].brakeTorque` | Brake torque per wheel (front left) | Nm* |
| `brakeTorqueFR` | `CPHYS.wheels[1].brakeTorque` | Brake torque per wheel (front right) | Nm* |
| `brakeTorqueRL` | `CPHYS.wheels[2].brakeTorque` | Brake torque per wheel (rear left) | Nm* |
| `brakeTorqueRR` | `CPHYS.wheels[3].brakeTorque` | Brake torque per wheel (rear right) | Nm* |
| `turboboost` | `CAR.turboBoost` | Turbo boost, from 0 upwards | bar |

### `gps` (selectable rate)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `posx` | `CAR.position.x` | World position, X axis | m* |
| `posy` | `CAR.position.z` | World position, horizontal Y axis (AC Z axis) | m* |
| `posz` | `CAR.position.y` | Height (AC Y axis) | m* |
| `velx` | `CAR.localVelocity.z` | Forward velocity, in the car frame | m/s* |
| `vely` | `CAR.localVelocity.x` | Lateral velocity, in the car frame | m/s* |
| `velz` | `CAR.localVelocity.y` | Vertical velocity, in the car frame | m/s* |
| `carHeading` | `CAR.compass` | Heading; recorded range −180 to 180 | deg |
| `pitchrate` | `CAR.localAngularVelocity.z` | Rotation around the forward axis; likely roll rate (see caveats) | rad/s* |
| `pitchangle` | `CAR.look.y` | Sine of the pitch angle relative to the world, track slope included (see caveats) | — |
| `rollrate` | `CAR.localAngularVelocity.x` | Rotation around the lateral axis; likely pitch rate (see caveats) | rad/s* |
| `rollangle` | `CAR.side.y` | Sine of the roll angle relative to the world, track camber included (see caveats) | — |
| `yawrate` | `CAR.localAngularVelocity.y` | Rotation around the vertical axis | rad/s* |

### `tires_dyn` (selectable rate)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `wheelspeedFL` | `CAR.wheels[0].angularSpeed` | Wheel angular speed; × loaded radius gives the ground speed (front left) | rad/s* |
| `wheelspeedFR` | `CAR.wheels[1].angularSpeed` | Wheel angular speed; × loaded radius gives the ground speed (front right) | rad/s* |
| `wheelspeedRL` | `CAR.wheels[2].angularSpeed` | Wheel angular speed; × loaded radius gives the ground speed (rear left) | rad/s* |
| `wheelspeedRR` | `CAR.wheels[3].angularSpeed` | Wheel angular speed; × loaded radius gives the ground speed (rear right) | rad/s* |
| `ndslipfl` | `CAR.wheels[0].ndSlip` | Normalized slip (front left) | —* |
| `ndslipfr` | `CAR.wheels[1].ndSlip` | Normalized slip (front right) | —* |
| `ndsliprl` | `CAR.wheels[2].ndSlip` | Normalized slip (rear left) | —* |
| `ndsliprr` | `CAR.wheels[3].ndSlip` | Normalized slip (rear right) | —* |
| `tireloadfl` | `CAR.wheels[0].load` | Vertical tyre load (front left) | N |
| `tireloadfr` | `CAR.wheels[1].load` | Vertical tyre load (front right) | N |
| `tireloadrl` | `CAR.wheels[2].load` | Vertical tyre load (rear left) | N |
| `tireloadrr` | `CAR.wheels[3].load` | Vertical tyre load (rear right) | N |
| `tireloadedradfl` | `CAR.wheels[0].tyreLoadedRadius` | Loaded tyre radius (front left) | m* |
| `tireloadedradfr` | `CAR.wheels[1].tyreLoadedRadius` | Loaded tyre radius (front right) | m* |
| `tireloadedradrl` | `CAR.wheels[2].tyreLoadedRadius` | Loaded tyre radius (rear left) | m* |
| `tireloadedradrr` | `CAR.wheels[3].tyreLoadedRadius` | Loaded tyre radius (rear right) | m* |
| `tireslipanglefl` | `CAR.wheels[0].slipAngle` | Slip angle (front left) | deg |
| `tireslipanglefr` | `CAR.wheels[1].slipAngle` | Slip angle (front right) | deg |
| `tireslipanglerl` | `CAR.wheels[2].slipAngle` | Slip angle (rear left) | deg |
| `tireslipanglerr` | `CAR.wheels[3].slipAngle` | Slip angle (rear right) | deg |
| `tireslipratiofl` | `CAR.wheels[0].slipRatio` | Slip ratio (front left) | —* |
| `tireslipratiofr` | `CAR.wheels[1].slipRatio` | Slip ratio (front right) | —* |
| `tireslipratiorl` | `CAR.wheels[2].slipRatio` | Slip ratio (rear left) | —* |
| `tireslipratiorr` | `CAR.wheels[3].slipRatio` | Slip ratio (rear right) | —* |
| `tirelongforcefl` | `CAR.wheels[0].fx` | Longitudinal tyre force (front left) | N* |
| `tirelongforcefr` | `CAR.wheels[1].fx` | Longitudinal tyre force (front right) | N* |
| `tirelongforcerl` | `CAR.wheels[2].fx` | Longitudinal tyre force (rear left) | N* |
| `tirelongforcerr` | `CAR.wheels[3].fx` | Longitudinal tyre force (rear right) | N* |
| `tirelatforcefl` | `CAR.wheels[0].fy` | Lateral tyre force (front left) | N* |
| `tirelatforcefr` | `CAR.wheels[1].fy` | Lateral tyre force (front right) | N* |
| `tirelatforcerl` | `CAR.wheels[2].fy` | Lateral tyre force (rear left) | N* |
| `tirelatforcerr` | `CAR.wheels[3].fy` | Lateral tyre force (rear right) | N* |

### `gforce` (selectable rate)

| Channel | Source (CSP) | Description | Unit |
|---|---|---|---|
| `cgaccellat` | `CAR.acceleration.x` | Lateral acceleration | G |
| `cgaccellong` | `CAR.acceleration.z` | Longitudinal acceleration | G |
| `cgaccelvert` | `CAR.acceleration.y` | Vertical acceleration, gravity excluded | G |

### `susp` (selectable rate)

| Channel | Source | Description | Unit |
|---|---|---|---|
| `rideheightfront` | `CAR.rideHeight[0]` | Front ride height | m* |
| `rideheightrear` | `CAR.rideHeight[1]` | Rear ride height | m* |
| `cgheight` | `CAR.cgHeight` | Centre of gravity height | m* |
| `susptravelfl` | `CAR.wheels[0].suspensionTravel` | Suspension travel (front left) | m* |
| `susptravelfr` | `CAR.wheels[1].suspensionTravel` | Suspension travel (front right) | m* |
| `susptravelrl` | `CAR.wheels[2].suspensionTravel` | Suspension travel (rear left) | m* |
| `susptravelrr` | `CAR.wheels[3].suspensionTravel` | Suspension travel (rear right) | m* |
| `tirealignntrqfl` | `CAR.wheels[0].mz` | Self-aligning torque (front left) | Nm* |
| `tirealignntrqfr` | `CAR.wheels[1].mz` | Self-aligning torque (front right) | Nm* |
| `tirealignntrqrl` | `CAR.wheels[2].mz` | Self-aligning torque (rear left) | Nm* |
| `tirealignntrqrr` | `CAR.wheels[3].mz` | Self-aligning torque (rear right) | Nm* |
| `damperTravelFL` | Python app: `ac.ext_getDamperTravel(0)` × 1000 | Damper travel (front left) | mm |
| `damperTravelFR` | Python app: `ac.ext_getDamperTravel(1)` × 1000 | Damper travel (front right) | mm |
| `damperTravelRL` | Python app: `ac.ext_getDamperTravel(2)` × 1000 | Damper travel (rear left) | mm |
| `damperTravelRR` | Python app: `ac.ext_getDamperTravel(3)` × 1000 | Damper travel (rear right) | mm |
| `damperTravelHF` | Python app: `ac.ext_getDamperTravel(4)` × 1000 | Heave damper travel, front and rear | mm |
| `damperTravelHR` | Python app: `ac.ext_getDamperTravel(5)` × 1000 | Heave damper travel, front and rear | mm |
| `caster` | `CAR.caster` | Caster angle | deg |
| `camberfl` | `CAR.wheels[0].camber` | Camber angle (front left) | deg |
| `camberfr` | `CAR.wheels[1].camber` | Camber angle (front right) | deg |
| `camberrl` | `CAR.wheels[2].camber` | Camber angle (rear left) | deg |
| `camberrr` | `CAR.wheels[3].camber` | Camber angle (rear right) | deg |
| `toefl` | `CAR.wheels[0].toeIn` | Toe angle; front wheels include steering (front left) | deg |
| `toefr` | `CAR.wheels[1].toeIn` | Toe angle; front wheels include steering (front right) | deg |
| `toerl` | `CAR.wheels[2].toeIn` | Toe angle; front wheels include steering (rear left) | deg |
| `toerr` | `CAR.wheels[3].toeIn` | Toe angle; front wheels include steering (rear right) | deg |
