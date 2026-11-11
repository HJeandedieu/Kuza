# Kuza Plant Photo Assessment Guide

**Owner:** Hashimweyesu Jean de Dieu  
**Status:** Draft for team review

Kuza uses a maize photo to flag a possible condition. Jean and Eunice confirm the supported conditions using the available labeled images. Keep the supported list and model version together.

| Situation | Result |
| --- | --- |
| Photo is too blurry, dark or poorly framed to assess | Ask the farmer to retake it and give a clear reason. |
| Photo is usable but the model is uncertain | Say the photo could not support a confident assessment. |
| A supported condition meets its approved confidence threshold | Return the possible condition and model version. |

The backend checks photo consent before calling the service. A service failure is shown as unavailable. The farmer can still submit symptoms. See the [shared API guide](../API-and-Communication-Guide.md) for the reply format and the [AI testing guide](AI-Data-and-Testing-Guide.md) for how a condition is approved.
