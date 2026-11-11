# Kuza Frontend Build Guide

**Owner:** Ishimwe Jenny Miriotta  
**Status:** Draft for team review

Use the [screen designs](Screen-Designs-and-Farmer-Journey.md) for layout and the [shared API guide](../API-and-Communication-Guide.md) for data.

1. Build sign-in and field setup. Check required inputs before submission and show any error returned by the backend next to the relevant field. Keep entered details when a request fails.
2. Build the dashboard. Display the reason and source returned with each task. Label simulated and outdated readings. Keep basic tasks visible when weather or sensor information is unavailable.
3. Build plant review. Let the farmer submit symptoms alone. Send a photo only after the farmer gives consent. Show upload progress and handle assessed, uncertain, retake, unavailable and symptoms-only replies.
4. Show harvest and storage advice when supplied by the backend.

Check keyboard navigation, readable labels, visible focus, and phone layouts. Test loading, empty and error states using the shared API examples. Measure dashboard and photo response times once the SRS targets are agreed.

Record the framework, local setup and hosting instructions once Jenny and Angella confirm them.
