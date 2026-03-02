# Integration Test Cases

The following integration tests verify system behavior across components including:

Sensor → Data Ingestion → Rules Engine → Dashboard → Alert System → Event Log

---

## IT-01 – Geofence Breach Alert

**Test Case ID:** IT-01  

**Test Case Description:**  
Verifies that when buoy coordinates move outside the configured geofence, the system generates a critical alert, updates the dashboard, logs an event, and triggers notification services.

**Testing Prerequisites:**
- Dashboard running
- Geofence boundaries configured
- Alert system in test mode
- Event logging enabled

**Testing Steps:**
1. Send valid payload with coordinates inside geofence.
2. Confirm dashboard shows normal status.
3. Send payload with coordinates outside geofence.
4. Observe dashboard and alert behavior.
5. Verify event log entry.
6. Verify notification captured by alert service.

**Input Data:**
- Payload A: Valid coordinates inside region.
- Payload B: Coordinates outside allowed boundary.

**Expected Result:**
- Critical alert banner displayed.
- Map marker turns red.
- Event logged with timestamp and coordinates.
- Notification successfully triggered.

---

## IT-02 – Spike Detection Validation

**Test Case ID:** IT-02  

**Test Case Description:**  
Validates spike detection logic and color-coded dashboard updates.

**Testing Prerequisites:**
- Rolling baseline calculation enabled
- Dashboard trend charts active
- Event logging enabled

**Testing Steps:**
1. Send 10 steady readings to establish baseline (e.g., water temp 10°C).
2. Send reading at +60% of baseline.
3. Send reading at +120% of baseline.
4. Observe UI changes and event logs.

**Input Data:**
- Baseline readings: 10°C
- Spike 1: 16°C (+60%)
- Spike 2: 22°C (+120%)

**Expected Result:**
- +60% reading marked Yellow.
- +120% reading marked Red.
- Both spikes logged as events.
- Trend chart visually highlights spike points.

---

## IT-03 – Critical Water Temperature Alert

**Test Case ID:** IT-03  

**Test Case Description:**  
Ensures system detects and responds to dangerous water temperature levels.

**Testing Prerequisites:**
- Water temperature threshold rule active
- Alert system in test mode
- Event logging enabled

**Testing Steps:**
1. Send payload with water temperature -5°C.
2. Confirm normal display.
3. Send payload with water temperature -31°C.
4. Observe alert and logging behavior.

**Input Data:**
- Payload A: waterTemp = -5°C
- Payload B: waterTemp = -31°C

**Expected Result:**
- Critical alert banner displayed.
- Water temperature card turns red.
- Event logged as Critical.
- Notification triggered successfully.

---

## IT-04 – Oxygen Saturation Threshold Verification

**Test Case ID:** IT-04  

**Test Case Description:**  
Verifies oxygen level interpretation across Normal, Warning, and Critical states.

**Testing Prerequisites:**
- Oxygen threshold logic configured
- Dashboard metrics visible
- Event logging enabled

**Testing Steps:**
1. Send oxygen value 85%.
2. Send oxygen value 75%.
3. Send oxygen value 65%.
4. Observe UI and alert behavior.

**Input Data:**
- 85%
- 75%
- 65%

**Expected Result:**
- 85% displays Green (Normal).
- 75% displays Yellow and logs Warning event.
- 65% displays Red, triggers Critical alert banner, logs event, and sends notification.
