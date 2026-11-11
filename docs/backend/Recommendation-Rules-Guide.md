# Kuza Recommendation Rules Guide

**Owner:** Mwizerwa Sano Angella  
**Crop review:** Atete Kabundi Eunice  
**Status:** Draft for team review

Start with the estimated maize stage and its basic tasks. Use relevant weather, observations and sensor readings to adjust advice only when the rule's conditions are met. Every recommendation carries an action, reason and source from the [Maize Reference Guide](../hardware/Maize-Reference-Guide.md).

| Example to check | Expected behavior |
| --- | --- |
| Wet soil and current forecast showing rain | Show the reviewed advice for waiting before irrigation and explain both inputs. |
| Forecast unavailable or outdated | Show basic crop-stage tasks. Mark the forecast status and avoid relying on it for a current weather decision. |
| Sensor unavailable | Keep basic tasks and use any applicable rules supported by the remaining current inputs. |
| Inputs disagree | Identify the conflict and use basic guidance when the inputs cannot support a more specific recommendation. |
| Harvest or storage stage | Show the applicable sourced harvest or storage advice. |

For each rule, record its crop stage, required inputs, what counts as current information, action, reason, source, and a test example. Eunice reviews source references and thresholds before Angella enables the rule. The examples above describe product behavior and still need approved crop references.
