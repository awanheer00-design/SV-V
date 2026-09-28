| ID | Operation | Input | Post-Condition |
| --- | --- | --- | --- |
| **OP-01** | **`PerformSelfCheck`** | `PowerOn` (Boolean) | If all essential sensors and devices respond correctly, `SelfCheckStatus` = SUCCESS and `SystemState` = MONITORING. Otherwise, `SelfCheckStatus` = FAIL and `SystemState` = ERROR_HALT. |
| **OP-02** | **`RecordArtifactProfile`** | `ArtifactID`, `TempRange`, `HumidityRange`, `VibThreshold` | `CurrentArtifact` is updated, environmental limits are stored, `ProfileLoaded` = TRUE, and `ProfileStatus` = LOADED. |
| **OP-03** | **`ActivateConservation`** | None | `SystemState` = CONSERVATION_ACTIVE and `EnvironmentalControls` = ACTIVE. |
| **OP-04** | **`AdjustTemperature`** | `CurrentTemp` | System triggers temperature adjustment (`ControlCommand` = HEAT/COOL/NONE), starts recovery timer, and sets `ArtifactSafetyVerified` = FALSE. |
| **OP-05** | **`VerifyEnvironmentalRecovery`** | `CurrentTemp`, `CurrentHumidity`, `ElapsedTime` | If parameters return to safe limits within the recovery period, `ArtifactSafetyVerified` = TRUE. If timeout occurs, `SystemState` = PROTECTION_MODE. |
| **OP-06** | **`EnterProtectionMode`** | `TriggerCause` | `SystemState` = PROTECTION_MODE, light exposure is reduced, auxiliary controls are activated, and operator alert is generated. |
| **OP-07** | **`HandleVibrationResponse`** | `VibrationReading` | `SystemState` = VIBRATION_RESPONSE, risk-increasing activities are suspended, and stabilization timer is reset. |
| **OP-08** | **`VerifyStabilization`** | `VibrationReading`, `ContinuousStableTime` | If vibration remains below threshold for the stabilization period, `SystemState` = CONSERVATION_ACTIVE and normal operation resumes. |
| **OP-09** | **`SuspendConservation`** | `DoorSensorState` (OPEN) | `SystemState` = MONITORING and active conservation is immediately halted. |
| **OP-10** | **`SwitchPowerSource`** | `MainPowerState`, `EmergencyPowerAvailable` | If backup power is available, `PowerSource` = EMERGENCY_BATTERY. Otherwise, system executes safe shutdown. |
| **OP-11** | **`ExecuteSafeShutdown`** | `IncidentDetails` | Power loss incident is appended to system log and `SystemState` = OFF. |
| **OP-12** | **`AuthorizeArtifactRemoval`** | `OperatorRequest` | If chamber is safe and not in protection/vibration response, `RemovalPermission` = GRANTED and `CurrentArtifact` = NULL. Otherwise, permission is DENIED. |
