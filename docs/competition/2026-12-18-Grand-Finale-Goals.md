# Kuza Grand Finale Goals — 18 December 2026

**Owner:** Jean de Dieu  
**Applies if:** Kuza advances through the 14 December semi-final

The public calendar lists a **14 December semi-final** with a developed MVP demonstration, seven minutes to pitch and three minutes for questions. The **18 December Grand Finale** brings together the Top 10 for 15-minute presentations and five minutes for questions. Use the invitations to confirm event setup and submission details. [Official competition calendar](https://www.codeforimpact.rw/about)

## First checkpoint — working demo for 14 December

A judge should be able to follow a complete maize farmer journey on a hosted, phone-friendly website. Add a field, see the estimated stage and weekly tasks, show a weather-adjusted recommendation with its reason and source, submit symptoms and an optional plant photo, and open harvest or storage advice for a sample late-season field.

| Owner | Deliver for the semi-final | Check before presenting |
| --- | --- | --- |
| **Jenny — Frontend** | Connect the mobile screens for the full farmer journey. | Run the journey on a phone from a fresh demo account, including the uncertain photo result. |
| **Angella — Backend** | Host the backend, save fields and reviews, return sourced advice, and prepare a reset for sample data. | Run the demo after a reset and check behavior when weather or AI is unavailable. |
| **Jean — AI engine** | Connect maize photo assessment and prepare the model test summary and sample retraining walkthrough. | Show a supported example and a retake or uncertain result. Record the test image count and results for the version in use. |
| **Eunice — Hardware and crop data** | Review the maize sources and provide labeled simulated readings. Bring a physical moisture-sensor example if it passes bench tests. | Trace the demo advice to its source and verify the simulator can support the demo independently. |

Aim to have the complete flow connected by **7 December**. By **11 December**, run the [System Testing Guide](../System-Testing-Guide.md), record results, and prepare screenshots or a recording for the main demo. Jean reviews the evidence and signs off before the semi-final.

## Grand Finale — improve the demo and show the evidence

- **15 December — Act on semi-final feedback.** Jean records what judges asked and assigns each important fix. Keep the working maize journey as the release scope.
- **16 December — Verify fixes.** Jenny repeats the mobile flow. Angella verifies hosting and reset. Jean rechecks AI results if the model changed. Eunice rechecks crop sources and the sensor example.
- **17 December — Rehearse and sign off.** Run the presentation and Q&A with the hosted site and the backup. Prepare the same sample field and reset instructions for the exhibition. Jean confirms what the team can demonstrate and support with evidence.
- **18 December — Present.** Show the farmer journey, what the team tested, who would pay, and how a future farm trial would measure outcomes. Clearly identify sample data and simulated sensor readings.

## Evidence to bring

| Evidence | Owner |
| --- | --- |
| Hosted link, demo account, seeded fields and reset steps | Angella |
| Phone walkthrough, screenshots or recording, and website speed results under recorded test conditions | Jenny and Angella |
| Photo assessment results, limits and sample retraining walkthrough | Jean |
| Sources for maize advice, sensor test results and simulator backup | Eunice |
| Business model and a trial plan for measuring water use, planning time and crop outcomes | Jean |

Keep website timing and model results tied to the conditions tested. Present farm outcomes as trial goals until the team has measured them in use. The [SRS](../SRS.md) and [API and Communication Guide](../API-and-Communication-Guide.md) remain the references for implementation.
