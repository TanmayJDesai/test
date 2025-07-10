# MORA InfluxDB Schema

## Bucket Structure
**Device Management Bucket:** `MoraDeviceBinding_V2_4`
**Signal Resource Management Bucket:** `MoraSignalResourceBinding_V2_4`

## Operations from XSD (22 total)

### MDevM Operations (11):
1. `getDeviceDescription`
2. `getDeviceStatus`
3. `getFileList`
4. `getCurrentMoraConfiguration`
5. `setCurrentMoraConfiguration`
6. `getAvailableMoraConfigurations`
7. `runBuiltInTest`
8. `getBuiltInTestResults`
9. `sendCommand`
10. `pullFile`
11. `deleteFile`

### MSRM Operations (11):
1. `getSignalPorts`
2. `getSignalPortDescription`
3. `getSignalPortDefaultPerformanceData`
4. `reserveSignalPort`
5. `releaseSignalPort`
6. `getSignalPortReservations`
7. `getStaticExternalConnectionMap`
8. `getStaticInternalConnectionMap`
9. `getInternalReferenceConnections`
10. `getAntennaArrays`
11. `getManifoldBands`

## Bucket/Measurement/Tags/Fields Structure

### Bucket: `MoraDeviceBinding_V2_4` (MDevM Operations)

#### Measurement: `getDeviceDescription`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - moraDevice_t.id
- `type` (string) - moraDevice_t.type (OTH, RCD, RHD, SDR)
- `subType` (string) - moraDevice_t.subType (RXO, TXO, TOR, TAR)
- `serviceName` (string) - moraDevice_t.serviceName

**Fields:**
- `id` (integer) - moraDevice_t.id
- `versionInfoUrl` (string) - moraDevice_t.versionInfoUrl

#### Measurement: `getDeviceStatus`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `state` (string) - deviceStatus_t.state (OPERATIONAL, STANDBY, TRANSMIT_INHIBIT, FAULT, ZEROIZED, MAINTENANCE_MODE, SANITIZED)
- `softwareVersion` (string) - deviceStatus_t.softwareVersion

**Fields:**
- `timeSynchronized` (boolean) - deviceStatus_t.timeSynchronized
- `calibrated` (boolean) - deviceStatus_t.calibrated
- `builtInTestSummaryResult` (string) - deviceStatus_t.builtInTestSummaryResult (PASS, IN-PROGRESS, FAIL)
- `powerConsumption` (float) - deviceStatus_t.powerConsumption (watts)
- `batteryRemaining` (float) - deviceStatus_t.batteryRemaining (0-100%)
- `temperature` (float) - deviceStatus_t.temperature (Celsius)
- `diskSpaceAvailable` (float) - deviceStatus_t.diskSpaceAvailable (kilobytes)
- `cpuUsage` (float) - deviceStatus_t.cpuUsage (0-100%)
- `memoryUsage` (float) - deviceStatus_t.memoryUsage (0-100%)
- `description` (string) - deviceStatus_t.description

#### Measurement: `getFileList`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `fileName` (string) - moraFile_t.fileName
- `type` (string) - moraFile_t.type (UNSPECIFIED, ERROR_LOG, SYSTEM_LOG, LOCATION_LOG, BIT_RESULTS, CALIBRATION, CONFIGURATION, APPLICATION, PROFILE)
- `path` (string) - moraFile_t.path

**Fields:**
- `size` (integer) - moraFile_t.size (bytes)
- `dateModified` (string) - moraFile_t.dateModified (ISO format)

#### Measurement: `getCurrentMoraConfiguration`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier

**Fields:**
- `id` (integer) - Current MORA configuration ID (gt0Int_t)

#### Measurement: `setCurrentMoraConfiguration`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `operation_result` (string) - Success/Error status

**Fields:**
- `id` (integer) - moraConfiguration_t.id being set
- `error_code` (string) - Error code if operation failed

#### Measurement: `getAvailableMoraConfigurations`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `configuration_id` (string) - moraConfiguration_t.id as tag
- `name` (string) - moraConfiguration_t.name

**Fields:**
- `id` (integer) - moraConfiguration_t.id
- `supportedSignalPortCount` (integer) - Count of signalPortIds_t.signalPortId

#### Measurement: `runBuiltInTest`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `operation_result` (string) - Success/Error status

**Fields:**
- `error_code` (string) - Error code if operation failed
- `test_initiated` (boolean) - Whether test was successfully started

#### Measurement: `getBuiltInTestResults`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `testName` (string) - builtInTestResult_t.testName
- `testResult` (string) - builtInTestResult_t.testResult (PASS, FAIL)

**Fields:**
- `testResultDescription` (string) - builtInTestResult_t.testResultDescription

#### Measurement: `sendCommand`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `command` (string) - Command sent (OPERATE, STANDBY, TRANSMIT_INHIBIT, POWER_ON, SHUT_DOWN, RESTART, MAINTENANCE_MODE, ZEROIZE, SANITIZE)
- `operation_result` (string) - Success/Error status

**Fields:**
- `error_code` (string) - Error code if command failed
- `command_executed` (boolean) - Whether command was successfully executed

#### Measurement: `pullFile`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `fileName` (string) - moraFile_t.fileName being pulled
- `operation_result` (string) - Success/Error status

**Fields:**
- `fileSize` (integer) - moraFile_t.size (bytes)
- `error_code` (string) - Error code if operation failed
- `transfer_successful` (boolean) - Whether file was successfully transferred

#### Measurement: `deleteFile`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `fileName` (string) - moraFile_t.fileName being deleted
- `operation_result` (string) - Success/Error status

**Fields:**
- `error_code` (string) - Error code if operation failed
- `file_deleted` (boolean) - Whether file was successfully deleted

#### Measurement: `getSignalPorts`
**Bucket:** `MoraSignalResourceBinding_V2_4`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - signalPort_t.id as tag
- `type` (string) - signalPort_t.type (ARX, ATX, ATR, DRX, DTX, DTR, ARI, ARO, DRI, DRO)
- `subType` (string) - signalPort_t.subType (RSC, ISC, BSC, RMC, IMC, BMC, RFS, IFS, BBS, OSC, CLK)
- `role` (string) - signalPort_t.role (PRODUCER, CONSUMER, BOTH)

**Fields:**
- `id` (integer) - signalPort_t.id
- `rxDelay` (integer) - signalPort_t.rxDelay (femtoseconds)
- `txDelay` (integer) - signalPort_t.txDelay (femtoseconds)
- `minPower` (integer) - signalPort_t.minPower (dBm)
- `maxPower` (integer) - signalPort_t.maxPower (dBm)
- `minVoltage` (integer) - signalPort_t.minVoltage (Volts)
- `maxVoltage` (integer) - signalPort_t.maxVoltage (Volts)
- `rxFrequencyStart` (float) - signalPort_t.rxFrequencyRange.start (Hz)
- `rxFrequencyEnd` (float) - signalPort_t.rxFrequencyRange.end (Hz)
- `rxFrequencyResolution` (float) - signalPort_t.rxFrequencyRange.resolution (Hz)
- `txFrequencyStart` (float) - signalPort_t.txFrequencyRange.start (Hz)
- `txFrequencyEnd` (float) - signalPort_t.txFrequencyRange.end (Hz)
- `txFrequencyResolution` (float) - signalPort_t.txFrequencyRange.resolution (Hz)

#### Measurement: `getSignalPortDescription`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - signalPortDescription_t.signalPortId

**Fields:**
- `signalPortId` (integer) - signalPortDescription_t.signalPortId
- `hasRfConditioning` (boolean) - Whether rfConditioning exists
- `hasRfTranslation` (boolean) - Whether rfTranslation exists
- `hasSignalDomainConversion` (boolean) - Whether signalDomainConversion exists
- `subPortCount` (integer) - Number of subPorts

#### Measurement: `getSignalPortDefaultPerformanceData`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - portDefaultPerformanceData_t.signalPortId
- `signalDirection` (string) - signalPortPerformanceData_t.signalDirection (TX, RX)

**Fields:**
- `signalPortId` (integer) - portDefaultPerformanceData_t.signalPortId
- `frequency` (float) - signalPortPerformanceData_t.frequency (Hz)
- `gain` (float) - signalPortPerformanceData_t.gain (dB)
- `noiseFigure` (float) - signalPortPerformanceData_t.noiseFigure (dB)
- `inputSecondOrderInterceptPoint` (float) - signalPortPerformanceData_t.inputSecondOrderInterceptPoint (dBm)
- `inputThirdOrderInterceptPoint` (float) - signalPortPerformanceData_t.inputThirdOrderInterceptPoint (dBm)
- `input1dbCompressionPoint` (float) - signalPortPerformanceData_t.input1dbCompressionPoint (dBm)
- `powerSaturation` (float) - signalPortPerformanceData_t.powerSaturation (dBm)
- `signalRelatedSpurious` (float) - signalPortPerformanceData_t.signalRelatedSpurious (dBc)
- `internallyGeneratedSpurious` (float) - signalPortPerformanceData_t.internallyGeneratedSpurious (dBm)

#### Measurement: `reserveSignalPort`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - Signal port ID being reserved
- `operation_result` (string) - Success/Error status

**Fields:**
- `id` (integer) - reservationConfirmation_t.id
- `confirmationNumber` (integer) - reservationConfirmation_t.confirmationNumber
- `error_code` (string) - Error code if operation failed

#### Measurement: `releaseSignalPort`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - Signal port ID being released
- `operation_result` (string) - Success/Error status

**Fields:**
- `id` (integer) - reservationConfirmation_t.id
- `confirmationNumber` (integer) - reservationConfirmation_t.confirmationNumber
- `error_code` (string) - Error code if operation failed

#### Measurement: `getSignalPortReservations`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `signalPortId` (string) - signalPortReservation_t.signalPortId
- `clientComponentId` (string) - clientComponentIds_t.clientComponentId

**Fields:**
- `signalPortId` (integer) - signalPortReservation_t.signalPortId
- `reservation_active` (boolean) - Whether reservation is active

#### Measurement: `getStaticExternalConnectionMap`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `localSignalPortId` (string) - externalConnection_t.localSignalPortId
- `externalSignalPortId` (string) - externalConnection_t.externalSignalPortId
- `externalDeviceId` (string) - externalConnection_t.externalDevice.id
- `externalDeviceType` (string) - externalConnection_t.externalDevice.type
- `externalServiceName` (string) - externalConnection_t.externalDevice.serviceName

**Fields:**
- `localSignalPortId` (integer) - externalConnection_t.localSignalPortId
- `externalSignalPortId` (integer) - externalConnection_t.externalSignalPortId
- `gainDelta` (float) - externalConnection_t.gainDelta (dB)
- `delayDelta` (integer) - externalConnection_t.delayDelta (femtoseconds)

#### Measurement: `getStaticInternalConnectionMap`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `portId1` (string) - connection_t.portId1
- `portId2` (string) - connection_t.portId2

**Fields:**
- `portId1` (integer) - connection_t.portId1
- `portId2` (integer) - connection_t.portId2
- `gainDelta` (float) - connection_t.gainDelta (dB)
- `delayDelta` (integer) - connection_t.delayDelta (femtoseconds)

#### Measurement: `getInternalReferenceConnections`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `referencePortId` (string) - referenceConnection_t.referencePortId
- `association` (string) - referenceConnection_t.association (CONDUCTED_INJECTION, RADIATED_INJECTION, SELECTABLE_INJECTION, FUNCTIONALLY_DEPENDENT)

**Fields:**
- `referencePortId` (integer) - referenceConnection_t.referencePortId
- `associatedPortCount` (integer) - Count of signalPortIds_t.signalPortId

#### Measurement: `getAntennaArrays`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `arrayId` (string) - antennaArray_t.id
- `type` (string) - antennaArray_t.type (CIRCULAR, DISCRETE, CONFORMAL, LINEAR_2D, LINEAR_3D, COLUMN)
- `steeringControl` (string) - antennaArray_t.steeringControl (FIXED, MECHANICAL, BEAMFORMER)

**Fields:**
- `id` (integer) - antennaArray_t.id
- `azimuthStart` (float) - antennaArray_t.arrayFieldOfView.azimuthRange.azimuthStart (degrees)
- `azimuthStop` (float) - antennaArray_t.arrayFieldOfView.azimuthRange.azimuthStop (degrees)
- `elevationStart` (float) - antennaArray_t.arrayFieldOfView.elevationRange.elevationStart (degrees)
- `elevationStop` (float) - antennaArray_t.arrayFieldOfView.elevationRange.elevationStop (degrees)
- `elementCount` (integer) - Count of arrayElements_t.element

#### Measurement: `getManifoldBands`
**Bucket:** `mora_signal_resource`
**Tags:**
- `host` (string) - Host collecting data
- `device_endpoint` (string) - Device endpoint URL
- `device_id` (string) - Device identifier
- `bandId` (string) - manifoldBand_t.bandId
- `calibrationFileName` (string) - manifoldBand_t.spatialCalibration.fileName

**Fields:**
- `bandId` (integer) - manifoldBand_t.bandId
- `frequencyStart` (float) - manifoldBand_t.frequencyRange.start (Hz)
- `frequencyEnd` (float) - manifoldBand_t.frequencyRange.end (Hz)
- `frequencyResolution` (float) - manifoldBand_t.frequencyRange.resolution (Hz)
- `fieldOfViewAzimuthStart` (float) - manifoldBand_t.fieldOfView.azimuthRange.azimuthStart (degrees)
- `fieldOfViewAzimuthStop` (float) - manifoldBand_t.fieldOfView.azimuthRange.azimuthStop (degrees)
- `fieldOfViewElevationStart` (float) - manifoldBand_t.fieldOfView.elevationRange.elevationStart (degrees)
- `fieldOfViewElevationStop` (float) - manifoldBand_t.fieldOfView.elevationRange.elevationStop (degrees)
- `apertureChannelCount` (integer) - Count of apertureChannels_t.apertureChannel


