# Kuza Hardware Build and Testing Guide

**Owner:** Atete Kabundi Eunice  
**Status:** Draft for team review

The project materials report an Arduino, moisture sensors and wiring available for bench work. ESP32 and MQTT are the proposed direction for connected sensors. Record the exact parts, quantities, board, pin connections and power requirements before assembling the prototype.

1. Check each component and record which parts are available, tested or still needed.
2. Record readings under known wet and dry conditions. Repeat measurements and document the setup, soil conditions and reading unit. Use the actual measurement unit supported by the test setup.
3. Send a reading using the [shared API guide](../API-and-Communication-Guide.md). Check the device and field IDs, time, value, unit and source shown by Kuza.
4. Disconnect and reconnect the device. Verify that an old reading is marked outdated and that new readings resume. Repeat with a duplicate message.
5. Keep a simulator that sends the same fields with the source marked as simulated. Use it to check the website when a physical device is unavailable.

Record the setup, expected result, actual result and any issue for each bench check. This guide covers soil moisture readings for the first version.
