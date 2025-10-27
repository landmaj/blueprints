# INSPELNING Smart plug

## Reporting settings

Default reporting settings in Zigbee2MQTT for INSPELNING smart plug lead to delayed
updates of power consumption and energy usage, to the point of being almost useless.
The below settings provide a near real-time updates without overwhelming the network.

| Cluster                 | Attribute            | Min rep internval | Max rep interval | Min rep change |
|-------------------------|----------------------|-------------------|------------------|----------------|
| haElectricalMeasurement | activePower          | 2                 | 60               | 2              |
| haElectricalMeasurement | rmsCurrent           | 10                | 3600             | 2              |
| haElectricalMeasurement | rmsVoltage           | 10                | 3600             | 10             |
| haElectricalMeasurement | acPowerDivisor       | 10                | 3600             | 1              |
| seMetering              | currentSummDelivered | 10                | 3600             | 10             |
