# Kuza Backend and Data Guide

**Owner:** Mwizerwa Sano Angella  
**Status:** Draft for team review

Use the [shared API guide](../API-and-Communication-Guide.md) for request and reply formats. Use the [rules guide](Recommendation-Rules-Guide.md) for advice logic.

| Record | What it holds |
| --- | --- |
| Account and field | The farmer's account and field access, crop, location, planting information and current condition. |
| Plant review | Field, symptoms, photo consent, assessment status and model version when available. |
| Photo | The stored file reference when retention is approved. |
| Forecast | Field location, forecast period and fetch time. |
| Device and reading | Device assignment, measurement time, value, unit and physical or simulated source. |

Check field access before reading, changing or deleting records. Check consent before processing or storing a photo. Keep symptoms if photo assessment fails. When a stored photo is deleted, remove access to the file and verify it is unavailable. Confirm retention and training consent with Jean.

For setup, document the chosen framework, database, environment settings, how to start the server, and how to load sample fields. Keep credentials out of the repository. Verify a fresh setup can sign in, create a field, receive a sample reading and return guidance.
