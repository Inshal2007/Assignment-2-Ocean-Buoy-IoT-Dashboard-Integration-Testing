# Dashboard Functional Requirements

The following requirements define how buoy data is interpreted and displayed on the monitoring dashboard.

---

## R1 – Geofence Breach Detection

If the buoy’s latitude and longitude fall outside the configured geofence boundary:

- A Critical (Red) alert banner shall be displayed at the top of the dashboard.
- The buoy marker on the map shall turn red.
- The geofence status indicator shall display "Outside Allowed Region".
- An event entry shall be logged in the event history table.
- A notification shall be sent to the alerting system (email/SMS/webhook).

This requirement ensures the system detects anchor failure and buoy drift.

---

## R2 – Spike Detection for Sensor Readings

For all numeric sensor readings (wave height, water temperature, air temperature, oxygen):

- The system shall calculate a rolling baseline (average of recent readings).
- If a reading exceeds the baseline by more than 50% but less than or equal to 100%, it shall be marked Yellow.
- If a reading exceeds the baseline by more than 100%, it shall be marked Red.
- The spike shall be visually indicated on the metric card and trend chart.
- An event shall be recorded in the event history.

This requirement detects abnormal environmental fluctuations.

---

## R3 – Critical Water Temperature Threshold

If water temperature falls below -30°C:

- A Critical (Red) alert banner shall be displayed.
- The water temperature metric card shall turn red.
- A Critical event shall be logged.
- A notification shall be sent to the alerting system.

This requirement protects salmon from lethal freezing conditions.

---

## R4 – Oxygen Saturation Threshold Levels

Oxygen saturation shall be interpreted as follows:

- 80–100% → Normal (Green)
- 70–79.99% → Warning (Yellow), event logged
- Below 70% → Critical (Red), alert banner displayed and notification sent

The oxygen metric card shall reflect the correct color state.

This requirement ensures fish health is continuously monitored.

---

## R5 – Data Freshness and Integrity

If no valid data payload is received within 2 minutes:

- The Data Status indicator shall display Warning or Critical.
- The “Last Updated” timestamp shall visually indicate stale data.
- An event shall be logged indicating data delay.

If a payload contains missing or invalid fields:

- The payload shall be rejected.
- The dashboard shall not update values from that payload.
- An error event shall be logged.

This requirement ensures reliability and system integrity.
