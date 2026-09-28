| ID | Operation | Input | Post-Condition |
| --- | --- | --- | --- |
| **OP-01** | **`PerformSelfCheck`** | `PowerOn` (Boolean) | If all sensors and control devices respond correctly, `SelfCheckStatus` = SUCCESS and `SystemState` = MONITORING. Otherwise, `SelfCheckStatus` = FAIL and `SystemState` = ERROR_HALT. |
| **OP-02** | **`RecordArtifactProfile`** | `ArtifactID`, `TempRange`, `HumidityRange`, `VibThreshold` | `CurrentArtifact` is updated, `ActiveLimits` are stored, `ProfileLoaded` = TRUE, and `ProfileStatus` = LOADED. |
| **OP-03** | **`CheckDoorStatus`** | `DoorSensorSignal` | `DoorState` is updated to OPEN or CLOSED. If OPEN, active conservation remains blocked. |
| **OP-04** | **`ActivateConservation`** | None | `SystemState` = CONSERVATION_ACTIVE and `EnvironmentalControls` = ACTIVE. |
| **OP-05** | **`ReadSensors`** | Sensor readings (`Temperature`, `Humidity`, `Light`, `Vibration`) | System environment state variables are updated with current physical values. |
| **OP-06** | **`AdjustTemperature`** | `CurrentTemp` | System triggers heating/cooling command (`ControlCommand` = HEAT/COOL/NONE), starts recovery timer, and sets `ArtifactSafetyVerified` = FALSE. |
| **OP-07** | **`AdjustHumidity`** | `CurrentHumidity` | System triggers humidification/dehumidification command, starts recovery timer, and sets `ArtifactSafetyVerified` = FALSE. |
| **OP-08** | **`VerifyEnvironmentalRecovery`** | `CurrentTemp`, `CurrentHumidity`, `ElapsedTime` | If readings return to safe limits within the recovery period, `ArtifactSafetyVerified` = TRUE. If timeout occurs, `SystemState` = PROTECTION_MODE. |
| **OP-09** | **`EnterProtectionMode`** | `TriggerCause` | `SystemState` = PROTECTION_MODE, `LightExposure` is reduced, auxiliary controls are enabled, and `OperatorAlert` = ACTIVE. |
| **OP-10** | **`HandleVibrationResponse`** | `VibrationReading` | `SystemState` = VIBRATION_RESPONSE, risk-increasing activities are suspended, and stabilization timer is reset. |
| **OP-11** | **`VerifyStabilization`** | `VibrationReading`, `ContinuousStableTime` | If vibration remains below threshold for the required period, `SystemState` = CONSERVATION_ACTIVE and activities resume. Otherwise, system remains in VIBRATION_RESPONSE. |
| **OP-12** | **`SuspendConservation`** | `DoorSensorState` (OPEN) | `SystemState` = MONITORING and normal environmental regulation is suspended. |
| **OP-13** | **`SwitchPowerSource`** | `MainPowerState`, `EmergencyPowerAvailable` | If emergency power is available, `PowerSource` = EMERGENCY_BATTERY. Otherwise, system triggers `ExecuteSafeShutdown`. |
| **OP-14** | **`ExecuteSafeShutdown`** | `IncidentDetails` | Power loss incident is appended to `SystemLog` and `SystemState` = OFF. |
| **OP-15** | **`AuthorizeArtifactRemoval`** | `OperatorRequest` | If system is safe and not in protection/vibration response, `RemovalPermission` = GRANTED and `CurrentArtifact` = NULL. Otherwise, permission is DENIED. |
