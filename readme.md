# SOAP API Test Results - InfluxDB Schema

## Bucket: 
`MoraDeviceBinding_V2_4`

## Measurement: 
`deleteFile`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`getAvailableMoraConfigurations`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `configuration_id`
* Tag: `configuration_name`
* Tag: `configuration_files`
* Tag: `supported_signal_ports`

## Measurement: 
`getBuiltInTestResults`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`getCurrentMoraConfiguration`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `configuration_id`

## Measurement: 
`getDeviceDescription`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `device_id`
* Tag: `device_type`
* Tag: `device_subtype`
* Tag: `service_name`
* Tag: `version_info_url`

## Measurement: 
`getDeviceStatus`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `state`
* Tag: `software_version`
* Tag: `description`

## Measurement: 
`pullFile`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`pushFile`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`runBuiltInTest`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`sendCommand`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`

## Measurement: 
`setCurrentMoraConfiguration`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Bucket: 
`MoraSignalResourceBinding_V2_4`

## Measurement: 
`getAntennaArrays`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `array_id`
* Tag: `array_type`
* Tag: `steering_control`
* Tag: `azimuth_start`
* Tag: `azimuth_stop`
* Tag: `elevation_start`
* Tag: `elevation_stop`
* Tag: `element_id`
* Tag: `element_type`
* Tag: `frequency_start`
* Tag: `frequency_end`
* Tag: `boresight_gain`

## Measurement: 
`getInternalReferenceConnections`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `reference_port_id`
* Tag: `signal_port_ids`
* Tag: `association`

## Measurement: 
`getManifoldBands`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `band_id`
* Tag: `frequency_start`
* Tag: `frequency_end`
* Tag: `frequency_resolution`
* Tag: `calibration_file_name`
* Tag: `calibration_type`
* Tag: `calibration_size`
* Tag: `aperture_channel_id`
* Tag: `channel_description`
* Tag: `associated_signal_port`

## Measurement: 
`getSignalPortDefaultPerformanceData`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `signal_port_id`
* Tag: `signal_direction`
* Tag: `frequency`
* Tag: `gain`
* Tag: `noise_figure`
* Tag: `input_second_order_intercept_point`
* Tag: `input_third_order_intercept_point`
* Tag: `input_1db_compression_point`
* Tag: `power_saturation`
* Tag: `signal_related_spurious`
* Tag: `internally_generated_spurious`

## Measurement: 
`getSignalPortDescription`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `signal_port_id`
* Tag: `stage_number`
* Tag: `signal_direction`
* Tag: `gain_type`
* Tag: `minimum_gain`
* Tag: `maximum_gain`
* Tag: `filter_id`
* Tag: `filter_type`
* Tag: `filter_logic`
* Tag: `bandwidth`
* Tag: `sub_port_id`
* Tag: `sub_port_type`
* Tag: `channel_coherency`

## Measurement: 
`getSignalPortReservations`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`

## Measurement: 
`getSignalPorts`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `signal_port_id`
* Tag: `port_type`
* Tag: `port_subtype`
* Tag: `port_role`
* Tag: `rx_delay`
* Tag: `tx_delay`
* Tag: `min_power`
* Tag: `max_power`
* Tag: `min_voltage`
* Tag: `max_voltage`
* Tag: `rx_frequency_start`
* Tag: `rx_frequency_end`
* Tag: `tx_frequency_start`
* Tag: `tx_frequency_end`
* Tag: `antenna_resource`

## Measurement: 
`getStaticExternalConnectionMap`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `local_signal_port_id`
* Tag: `external_signal_port_id`
* Tag: `external_device`
* Tag: `gain_delta`
* Tag: `delay_delta`

## Measurement: 
`getStaticInternalConnectionMap`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `port_id_1`
* Tag: `port_id_2`
* Tag: `gain_delta`
* Tag: `delay_delta`

## Measurement: 
`releaseSignalPort`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`

## Measurement: 
`reserveSignalPort`
* Tag: `status_code`
* Tag: `raw_success`
* Tag: `plugin_success`
* Tag: `error_code`
* Tag: `error_message`
