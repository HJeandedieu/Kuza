# Kuza System Testing Guide

**Owner:** Hashimweyesu Jean de Dieu  
**Status:** Draft for team review

Use the [SRS](SRS.md) and [API and Communication Guide](API-and-Communication-Guide.md) to prepare a test environment with two farmer accounts, sample maize fields at different stages, a sample forecast, simulated moisture readings, and approved test photos. Keep sample data separate from farmer data.

| Check | What to do | Expected result | Who records it |
| --- | --- | --- | --- |
| Field setup | Sign in on a phone, add a field, then reopen it. Try opening it as the second farmer. | Details persist and the second farmer is refused access. | Jenny and Angella |
| Weekly advice | Load a wet field with rain expected. Repeat with weather and readings unavailable. | Advice shows its reason and source. Basic tasks remain available when inputs are missing. | Angella and Eunice |
| Harvest and storage | Open a sample field at the appropriate stage. | Relevant guidance appears with its source. | Jenny and Eunice |
| Plant review | Submit symptoms alone, then test a usable photo, a blurry photo, and an unavailable AI service. | The site shows the appropriate result or next step and keeps the symptoms. | Jenny and Jean |
| Photo consent | Send a photo without consent in the test environment, then delete a photo saved with consent. | The first photo is rejected before processing or storage. The deleted photo cannot be opened. | Angella |
| Sensor readings | Send a sample reading, repeat it, then send an older one. Stop the feed. | The source is visible, duplicates are ignored, and the last reading is marked outdated after the agreed limit. | Eunice and Angella |
| Speed | Measure dashboard and photo review on a phone using the agreed network and photo size. | Results meet the targets agreed in the SRS. | Jenny and Angella |

For each run, record the build version, sample data, expected and actual result, pass or fail, and who will fix any issue. Retest after a fix. Jean reviews the results with the owners before approving the build.
