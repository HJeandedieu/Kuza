# Kuza API and Communication Guide

**Status:** Draft for team review  
**Owner:** Mwizerwa Sano Angella  
**Related document:** [Kuza SRS](SRS.md)

This shared guide defines how Kuza's website, backend, AI service, and sensors exchange information. The paths and sample messages below are proposed contracts. The team will confirm them before integration.

| Connection | Protocol | Who reviews it |
| --- | --- | --- |
| Website to backend | HTTPS, with JSON for most messages and a file upload for photos | Jenny and Angella |
| Backend to AI service | Private HTTPS, with a file upload for the photo and a JSON reply | Angella and Jean de Dieu |
| Sensor or simulator to backend | MQTT over TLS, through a server that receives and forwards messages | Eunice and Angella |
| Backend to weather provider | HTTPS through the provider's API | Angella |

The website gets all farmer-facing information from the backend. The backend checks permissions, calls the other services, and prepares the guidance the website displays.

## Website and backend

Use `/api/v1` as the proposed base path. Requests for fields, guidance, and photos require a signed-in session. The backend checks that the farmer has access to the field or photo on every request.

| Request | What it does |
| --- | --- |
| `POST /api/v1/accounts` | Create a farmer account. |
| `POST /api/v1/session` | Sign in and start a session. |
| `DELETE /api/v1/session` | Sign out and end the session. |
| `POST /api/v1/fields` | Save a maize field and return its ID. |
| `GET /api/v1/fields` | List fields the farmer can access. |
| `GET /api/v1/fields/{fieldId}` | Return saved field details. |
| `GET /api/v1/fields/{fieldId}/guidance` | Return crop stage, weekly tasks, applicable harvest or storage advice, and the latest weather and sensor status. |
| `POST /api/v1/fields/{fieldId}/plant-reviews` | Save symptom answers and assess an optional photo. |
| `DELETE /api/v1/plant-reviews/{reviewId}/photo` | Delete a stored photo belonging to a review the farmer can access. |

### Field and guidance examples

A field request includes a name, crop, location, current condition, and either planting date or crop age in days.

```json
{
  "name": "North field",
  "crop": "maize",
  "location": { "latitude": -1.95, "longitude": 30.06 },
  "plantingDate": "2026-10-15",
  "currentCondition": "Soil is still wet"
}
```

Example guidance reply for that field:

```json
{
  "fieldId": "field_01",
  "growthStage": "vegetative",
  "weeklyTasks": [
    {
      "action": "Wait before irrigating.",
      "reason": "The soil is still wet and rain is expected.",
      "sourceId": "maize-water-example"
    }
  ],
  "harvestAndStorage": [],
  "weather": { "status": "current" },
  "soilMoisture": {
    "status": "current",
    "value": 32,
    "unit": "volumetric_percent",
    "measuredAt": "2026-11-11T08:30:00Z",
    "source": "simulated"
  }
}
```

The source ID in this example is a placeholder. In the product, it points to a reference in the maize guide. Weather and soil moisture can each be `current`, `outdated`, or `unavailable`. Return basic crop-stage guidance when either input is unavailable.

### Plant review and errors

The website submits symptom answers with or without a photo. For a photo upload, send the file, symptom answers, and photo consent in the same multipart request. If consent is declined, submit the symptoms alone. The backend checks consent before calling the AI service or saving the file. It rejects any photo sent without consent. Access to photo processing does not imply consent to use a photo for training.

The plant review reply includes `reviewId` and `assessmentStatus`. Use `assessed`, `uncertain`, `retake_required`, `unavailable`, or `no_photo`. Return the possible condition for `assessed` and an explanation or next step for the other results. If the AI call fails, keep the submitted symptoms and return `unavailable` so the website can explain what happened.

For failed website requests, return a short code and readable message. Use HTTP `400` for invalid input, `401` when sign-in is required, `403` for a refused request, and `404` for an unavailable record. Example:

```json
{
  "code": "photo_consent_required",
  "message": "Give consent to share a photo, or submit symptoms without it."
}
```

## Backend and AI service

The backend calls `POST /internal/v1/photo-assessments` with service credentials. It sends the photo and crop as a multipart upload. The service returns the model version and a result. For example:

```json
{
  "status": "retake_required",
  "possibleCondition": null,
  "reason": "The image is too blurry to assess.",
  "modelVersion": "maize-demo-01"
}
```

The AI service returns `assessed`, `uncertain`, or `retake_required`. The backend maps a timeout or service error to `unavailable`. Angella's rules can use the result with symptom answers and available weather when preparing farmer-facing guidance.

## Sensors and backend

A device or simulator publishes to `kuza/v1/devices/{deviceId}/readings`. The backend listens for these messages through the MQTT server. Give each sender credentials limited to its assigned topic. The backend checks that the device is linked to the stated field.

```json
{
  "readingId": "reading_001",
  "deviceId": "sim_01",
  "fieldId": "field_01",
  "measuredAt": "2026-11-11T08:30:00Z",
  "soilMoisture": { "value": 32, "unit": "volumetric_percent" },
  "source": "simulated"
}
```

Physical readings use the same fields with `source` set to `physical`. Eunice confirms the unit before integration. Check the timestamp, unit, and device assignment before using the reading. Ignore repeats with the same device and reading IDs. An older reading must not replace a newer reading on the dashboard. When a device stops sending, mark its last reading outdated once it passes the agreed age limit.

## Backend and weather provider

The backend sends the field's latitude and longitude to the weather provider and keeps the provider credentials on the server. Keep the time the forecast was fetched and the period it covers. When the provider is unavailable, show a saved forecast with its freshness status if one exists. Use basic crop-stage guidance when there is no current forecast to support a weather-based decision.

## Check the full flow together

1. **Weekly advice.** Add the sample field, send a simulated moisture reading, and supply a sample forecast with rain. Open the dashboard and check the advice, reason, reference, and simulation label. Repeat without a current forecast and check that basic tasks still appear.
2. **Plant photo.** Submit symptoms and a photo with consent. Check the backend's request to the AI service and the result on the website. Repeat with a blurry photo, with the service unavailable, and with symptoms alone.
3. **Access and data checks.** Try to access another account's field, send the same sensor reading twice, and delete a saved photo. Check that access is refused, the repeat is ignored, and the deleted photo is unavailable.

## Confirm before integration

- **Angella and Jenny** confirm session handling, account fields, symptom fields, upload size limits, and allowed image types.
- **Angella and Jean** confirm the AI service address, credentials, supported condition labels, and response time limit.
- **Angella and Eunice** confirm the MQTT server, device credentials, moisture unit, and how old a reading can be before it is marked outdated.
- **Angella** confirms the weather provider, forecast refresh interval, and forecast age limit.
