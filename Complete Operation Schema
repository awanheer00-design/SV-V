Here is Task 2 presented in the requested table format with the sections: **ID**, **Operation**, **Input**, and **Post-Condition**.

| ID | Operation | Input | Post-Condition |
| --- | --- | --- | --- |
| **OP-01** | **`PerformSelfCheck`** | `PowerOn` (Boolean)

 | If all sensors and control devices respond correctly, `SelfCheckStatus` = SUCCESS and `SystemState` = MONITORING. Otherwise, `SelfCheckStatus` = FAIL and `SystemState` = ERROR_HALT.

 |
| **OP-02** | **`RecordArtifactProfile`** | `ArtifactID`, `TempRange`, `HumidityRange`, `VibThreshold`<br> | `CurrentArtifact` is updated, `ActiveLimits` are stored, `ProfileLoaded` = TRUE, and `ProfileStatus` = LOADED.

 |
| **OP-03** | **`ActivateConservation`** | None | `SystemState` = CONSERVATION_ACTIVE and `EnvironmentalControls` = ACTIVE.

 |
| **OP-04** | **`AdjustTemperature`** | `CurrentTemp`<br> | System triggers heating/cooling command (`ControlCommand` = HEAT/COOL/NONE), starts recovery timer, and sets `ArtifactSafetyVerified` = FALSE.

 |
| **OP-05** | **`VerifyEnvironmentalRecovery`** | `CurrentTemp`, `CurrentHumidity`, `ElapsedTime`<br> | If readings return to safe limits within the recovery period, `ArtifactSafetyVerified` = TRUE. If timeout occurs, `SystemState` = PROTECTION_MODE.

 |
| **OP-06** | **`EnterProtectionMode`** | `TriggerCause`<br> | `SystemState` = PROTECTION_MODE, `LightExposure` is reduced, auxiliary controls are enabled, and `OperatorAlert` = ACTIVE.

 |
| **OP-07** | **`HandleVibrationResponse`** | `VibrationReading`<br> | `SystemState` = VIBRATION_RESPONSE, risk-increasing activities are suspended, and stabilization timer is reset.

 |
| **OP-08** | **`VerifyStabilization`** | `VibrationReading`, `ContinuousStableTime`<br> | If vibration remains below threshold for the required period, `SystemState` = CONSERVATION_ACTIVE and activities resume. Otherwise, system remains in VIBRATION_RESPONSE.

 |
| **OP-09** | **`SuspendConservation`** | `DoorSensorState` (OPEN)

 | `SystemState` = MONITORING and normal environmental regulation is suspended.

 |
| **OP-10** | **`SwitchPowerSource`** | `MainPowerState`, `EmergencyPowerAvailable`<br> | If emergency power is available, `PowerSource` = EMERGENCY_BATTERY. Otherwise, system triggers `ExecuteSafeShutdown`.

 |
| **OP-11** | **`ExecuteSafeShutdown`** | `IncidentDetails`<br> | Power loss incident is appended to `SystemLog` and `SystemState` = OFF.

 |
| **OP-12** | **`AuthorizeArtifactRemoval`** | `OperatorRequest`<br> | If system is safe and not in protection/vibration response, `RemovalPermission` = GRANTED and `CurrentArtifact` = NULL. Otherwise, permission is DENIED.

 |
