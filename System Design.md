# System Design
## IoT-Based Solar Storage Battery Compatibility Monitoring and Condition Assessment System

**Document status:** Proposed design — prototype not yet assembled.

## 1. System Architecture

The proposed system consists of two main paths:

**Energy path**

Solar Panel → Solar Charge Controller → Battery → DC Load

**Monitoring and data path**

Voltage, Current and Temperature Sensors → ESP32 → Wi-Fi → IoT Dashboard

The solar charge controller manages battery charging. The ESP32 reads sensor measurements, processes the data, evaluates configured thresholds, and sends available readings to the dashboard.

## 2. Proposed Components and Functions

| Component | Purpose |
|---|---|
| Small solar panel | Generates electrical energy |
| Compatible solar charge controller | Regulates charging according to battery requirements |
| Suitable low-voltage battery | Stores energy for the connected load |
| ESP32 Wi-Fi development board | Reads sensor data and transmits it wirelessly |
| Voltage sensor | Measures battery voltage |
| Charge/discharge current sensor | Measures current entering or leaving the battery |
| Temperature sensor | Measures battery temperature |
| Additional current sensor | Measures a defined leakage or standby current |
| DC load | Provides a controlled load for prototype testing |

Final component models, sensor ranges, wiring, and pin assignments will be confirmed during implementation.

## 3. Operating Sequence

1. The solar panel generates electrical energy.
2. The charge controller regulates charging of the compatible battery.
3. Sensors measure battery voltage, current, and temperature.
4. The additional current sensor measures the defined leakage or standby current under its intended test condition.
5. The ESP32 reads and processes the measurements.
6. Firmware checks readings against configured operating limits.
7. Data is transmitted over Wi-Fi to the selected IoT dashboard.
8. The dashboard displays readings, indicators, and alerts.

## 4. Compatibility Assessment

Battery and charge-controller compatibility will be assessed using documented specifications, including:

- Battery chemistry and nominal voltage
- Permitted charging voltage and current
- Charge-controller supported battery types and settings
- Battery operating temperature limits
- Manufacturer recommendations

Live sensor measurements help monitor operating conditions but do not independently prove that all aspects of battery compatibility are satisfied.

## 5. Battery Condition Indicators

### State of Charge (SOC)

SOC estimates the remaining charge in the battery. The estimation method will be selected according to the battery chemistry, available sensors, and calibration requirements.

### State of Health (SOH)

SOH estimates battery condition relative to its original or reference performance. A suitable method, such as a controlled capacity test, is required to validate the estimate.

### Usability Status

The proposed firmware will provide three status categories:

- **USABLE:** Measurements satisfy the configured operating and safety criteria.
- **LIMITED / INSPECT:** Charging is needed or a non-critical reading requires attention.
- **NOT USABLE:** A critical limit or fault condition requires the battery to be removed from service or inspected before further use.

Low SOC alone should generally trigger a charging warning rather than automatically indicating a faulty battery. Thresholds will follow the selected battery manufacturer's specifications.

## 6. Leakage or Standby Current

The additional current measurement must have a clearly defined purpose.

For this project, it may be used to measure unintended or standby current when the intended load is switched off. This is different from insulation leakage to ground. The circuit, sensor range, and measurement method will be selected to match the chosen definition.

## 7. Safety Considerations

- Use a charge controller compatible with the battery chemistry and voltage.
- Follow the battery manufacturer's charging and temperature limits.
- Use suitable wiring, fusing, and current ratings.
- Verify sensor voltage ranges and ESP32 input requirements before connecting circuits.
- Avoid unsafe short-circuit, overcharge, and deep-discharge tests.
- Test under controlled low-voltage conditions.

## 8. Validation Plan

After assembly, the system will be tested for:

- Voltage measurement accuracy against a reference multimeter
- Charge/discharge current measurement accuracy
- Temperature measurement consistency
- Leakage or standby current measurement under a defined condition
- Wi-Fi connectivity and dashboard data updates
- Status-indicator and alert behaviour
- Charging and discharging observations

Actual results will be added after testing.

## 9. Current Development Stage

The project is currently at the planning and system-design stage. Hardware integration, firmware implementation, dashboard connection, and validation remain to be completed.
