# Kuza Software Requirements Specification (SRS)

**Version:** 0.1  
**Status:** Draft for team review  
**Owner:** Hashimweyesu Jean de Dieu  
**Reviewers:** Ishimwe Jenny Miriotta, Mwizerwa Sano Angella, and Atete Kabundi Eunice

## Purpose and scope

Kuza helps farmers decide what their field needs next and why. It uses the crop's estimated growth stage, farmer observations, weather, and optional sensor readings to provide field-specific advice.

The first version supports maize through a mobile-friendly website. A farmer can add a field, see weekly tasks, review a plant photo and symptoms, and find harvest and storage guidance. Farmers can use Kuza without sensors. The website can display physical and simulated readings with clear labels.

Additional crops, SMS alerts, offline entry, and automatic irrigation and fertilizer delivery are planned for later versions.

## Frontend — Ishimwe Jenny Miriotta

| ID | What Kuza must do | How we check it |
| --- | --- | --- |
| FE-01 | Let a farmer sign in and add a maize field with its location, planting date or crop age, and current condition. | Register a field on a phone, reopen it, and check the saved details. |
| FE-02 | Show the estimated growth stage, season progress, weekly tasks, and the reason and source for each recommendation. | Open a sample field and find its next task, reason, and source. |
| FE-03 | Let farmers submit symptom answers and choose whether to share a plant photo. Show the assessment, an uncertain result, a retake prompt, or a message when the service is unavailable. | Test each result and confirm a farmer can submit symptoms after declining photo consent. |
| FE-04 | Show harvest and storage guidance when it applies. Label outdated weather and simulated readings. | Open a late-season field and check the labels on a field with an outdated forecast and simulated readings. |

## Backend and recommendation rules — Mwizerwa Sano Angella

| ID | What Kuza must do | How we check it |
| --- | --- | --- |
| BE-01 | Save accounts, fields, and plant reviews. Allow farmers to access only the fields they have permission to use. | Create a field under one account and confirm a second account cannot read or change it. |
| BE-02 | Estimate growth stage and use the maize reference guide, weather, observations, and sensor readings to recommend tasks. Return the reason and source for each recommendation. | Check agreed maize scenarios, including wet soil with rain expected, against the expected advice. |
| BE-03 | Keep showing basic crop-stage tasks when weather or sensor data is missing. Identify missing or outdated inputs. | Disable the weather feed and remove sensor readings. Check that basic tasks still appear and the missing inputs are identified. |
| BE-04 | Check consent before sending a photo for assessment or storing it. Support deletion of stored photos. | Decline consent and verify the photo was neither sent nor saved. Delete a saved test photo and verify it is no longer available. |

## AI engine — Hashimweyesu Jean de Dieu

| ID | What Kuza must do | How we check it |
| --- | --- | --- |
| AI-01 | Assess a usable maize photo for supported conditions. Return a possible condition or an uncertain result, with the model version. | Submit test photos and check the response and model version. |
| AI-02 | Ask for a retake when the photo is unusable. Show uncertainty when a usable photo cannot be assessed confidently. | Submit a blurry photo and a clear but ambiguous photo. Verify the two responses. |
| AI-03 | Measure performance on images kept separate from training. Record the test set size and the correct, incorrect, and uncertain results for each supported condition. | Review the test report for the model version used by Kuza. |

## Hardware and crop data — Atete Kabundi Eunice

| ID | What Kuza must do | How we check it |
| --- | --- | --- |
| HW-01 | Provide soil moisture readings with a device ID, field ID, time, unit, and a label identifying the source as physical or simulated. | Send a reading from each available source and check the value and label in Kuza. |
| HW-02 | Check physical readings under known conditions and document what happens when the device loses its connection. | Record readings under known wet and dry conditions, disconnect the device, and verify how Kuza shows the last reading. |
| HW-03 | Maintain a sourced maize guide covering growth stages, water needs, field observations, harvest, and storage. | Trace each sample recommendation to an entry and source in the guide. |

## Tech stack

The choices below describe the current design. The shared **API and Communication Guide** will hold the exact API addresses, message formats, access rules, and example exchanges.

| Part | Current direction | To confirm |
| --- | --- | --- |
| Frontend | Responsive website that connects to the backend over HTTPS. | Jenny confirms the framework and hosting with Angella. |
| Backend | HTTPS API, database, recommendation rules, and an external weather service. | Angella confirms the framework, database, hosting, and weather provider. |
| AI engine | A separate photo assessment service called by the backend over private HTTPS. This connection is proposed. | Jean confirms the model tools and hosting with Angella. |
| Hardware | The concept note proposes ESP32 and MQTT. Arduino, moisture sensors, and wiring were reported available for bench work. Physical devices and the simulator use the same reading format. | Eunice and Angella confirm the connected device and MQTT broker. |

## Decisions to confirm before approval

- **Current state.** Each owner marks their requirements as working, available but untested, or still to build.
- **Supported photo assessments.** Jean and Eunice confirm which maize conditions the available images can support. Jean records the minimum test results needed for each condition before Kuza shows it to a farmer.
- **Speed and freshness.** Jenny and Angella agree on dashboard and photo response targets. Angella and Eunice agree on when a forecast or reading should be marked outdated.
- **Photo handling.** Jean and Angella confirm whether photos need to be kept after assessment, for how long, and what consent is needed for training use.
- **Stack choices.** Each owner records their tools and confirms the connections with Angella.

## Project references

- Kuza concept note
- Submitted video script
