# Dashboard Design
## IoT-Based Solar Storage Battery Compatibility Monitoring and Condition Assessment System

**Document status:** Proposed dashboard design — not yet connected to live hardware.

## 1. Dashboard Purpose

The dashboard is designed to present battery operating measurements and condition indicators in a simple interface. It will help users identify charging requirements, abnormal measurements, and conditions that may require inspection.

The dashboard will receive sensor data from an ESP32 through Wi-Fi using a compatible IoT platform.

## 2. Main Dashboard Readings

| Parameter | Unit | Purpose |
|---|---|---|
| Battery voltage | V | Monitors battery terminal voltage |
| Charge/discharge current | A | Shows current entering or leaving the battery |
| Leakage/standby current | mA | Monitors current under a defined standby or leakage test condition |
| Battery temperature | °C | Monitors battery temperature |
| State of Charge (SOC) | % | Estimates remaining battery charge |
| State of Health (SOH) | % | Estimates battery condition using a suitable validated method |
| Compatibility status | Status | Indicates whether documented battery and controller requirements are satisfied |
| Usability status | Status | Indicates whether the battery appears usable or needs attention |

## 3. Proposed Dashboard Layout

### A. Live Sensor Monitoring

The main screen will show cards for:

- Battery voltage
- Charge/discharge current
- Leakage or standby current
- Battery temperature

The interface will show measurement units and, where possible, the latest update time.

### B. Battery Condition Indicators

**State of Charge (SOC)** will be displayed as a percentage and visual progress indicator.

**State of Health (SOH)** will be displayed as an estimated percentage only when an appropriate estimation method is implemented. The dashboard will identify the method and its limitations.

### C. Battery Usability Indicator

The proposed status indicator has three categories:

- **USABLE:** Available measurements meet the configured operating criteria.
- **LIMITED / INSPECT:** Charging or further inspection is required.
- **NOT USABLE:** A critical limit or fault condition has been detected.

A low SOC should normally result in a charging warning, not automatically classify the battery as faulty. Critical safety conditions will take priority over the general status.

### D. Compatibility Indicator

The dashboard will report whether the selected battery and charge controller satisfy the documented compatibility requirements.

This indicator will be based on battery and controller specifications, settings, and available verification. Sensor readings alone cannot establish full compatibility.

### E. Alerts and Trends

Planned features include:

- Low-charge warning
- Abnormal voltage warning
- High-temperature warning
- Current outside configured limits
- Excessive leakage or standby current under the defined test condition
- Historical readings and trends, if supported by the selected platform

## 4. Proposed Status Logic

| Condition | Dashboard response |
|---|---|
| Readings within configured limits | USABLE |
| Low SOC without a critical fault | LIMITED / CHARGE |
| Non-critical abnormal reading | LIMITED / INSPECT |
| Critical safety limit exceeded | NOT USABLE / INSPECT |
| Missing or invalid sensor data | SENSOR DATA UNAVAILABLE |

The firmware will apply battery-specific limits rather than relying on universal thresholds. Sensor failure or missing data must not be interpreted as proof that the battery is safe.

## 5. Proposed Data Flow

1. Sensors collect battery measurements.
2. ESP32 firmware reads and validates the measurements.
3. The firmware calculates supported indicators and evaluates thresholds.
4. ESP32 sends data over Wi-Fi.
5. The dashboard updates its readings and status indicators.
6. Alerts are displayed when configured conditions are met.

## 6. Implementation Plan

1. Select the IoT dashboard platform.
2. Define sensor data fields and units.
3. Develop ESP32 firmware and Wi-Fi transmission.
4. Create dashboard cards and status indicators.
5. Connect the dashboard to the ESP32.
6. Verify displayed readings against reference instruments.
7. Test alerts and usability-status rules.
8. Capture screenshots of the functioning dashboard.

## 7. Current Status and Limitations

This document describes the planned dashboard. The physical prototype, live sensor readings, and dashboard integration are not yet completed.

Any mock-up or example readings will be labelled as illustrative. Actual measurements, alerts, and test results will be documented only after implementation and validation.
