# Hypertension CDSS

An OCL collection for Hypertension (HTN) can be found here: TODO

## Prompts

The HTN.csv file contains details of hypertension prompts that are implemented in proforma at https://labs.openclinical.net/matt/dp_htn.

### Examples

Narrative descriptions of conditions that show and dont show the prompt are given along with links that contain the relevant data.

#### screening

##### htn_scrn_0

> all patients should have their blood pressure checked yearly

Running the protocol [without any data](https://labs.openclinical.net/matt/dp_htn) will show this alert because it is designed to be shown if you dont know the age of the person and you havent got a blood pressure reading.

Providing an [age less that 35](https://labs.openclinical.net/matt/dp_htn?age=30) means that the alert isnt shown even though there is no blood pressure reading.

Providing an [age more than 35](https://labs.openclinical.net/matt/dp_htn?age=60) means that the alert is shown.

Providing a [recent blood pressure reading](https://labs.openclinical.net/matt/dp_htn?_data={"dp_htn":{"sbp":[{"when": "2025-12-01T10:00", "value": 119}]}}) means that the alert isnt shown.

Providing an [old blood pressure reading](https://labs.openclinical.net/matt/dp_htn?_data={"dp_htn":{"sbp":[{"when": "2024-12-01T10:00", "value": 119}]}}) means that the alert is shown.

##### htn_scrn_1

> 	if a patients last blood pressure is close to 140/90, they should be screened more frequently

Providing an [eight month old blood pressure reading with sbp=138](https://labs.openclinical.net/matt/dp_htn?_data={"dp_htn":{"sbp":[{"when": "2025-02-01T10:00", "value": 138}], "dbp":[{"when": "2025-02-01T10:00", "value": 79}]}}) means that the alert is shown because it is between 135 and 140 which prompts a six month screening.

Providing an [eight month old blood pressure reading with dbp=87](https://labs.openclinical.net/matt/dp_htn?_data={"dp_htn":{"sbp":[{"when": "2025-02-01T10:00", "value": 132}], "dbp":[{"when": "2025-02-01T10:00", "value": 87}]}}) means that the alert is shown because it is between 135 and 140 which prompts a six month screening.

#### diagnosis

##### htn_diag_0

> patients with two consecutive blood pressure readings greater than 140/90 should have a diagnosis of hypertension

[Two high systolic blood pressure readings without hypertension listed as a condition](https://labs.openclinical.net/matt/dp_htn?_data={"dp_htn":{"sbp":[{"when": "2025-06-01T10:00", "value": 141}, {"when": "2025-12-01T10:00", "value": 143}], "dbp":[{"when": "2025-06-01T10:00", "value": 87}, {"when": "2025-12-01T10:00", "value": 87}]}}).  Add HTN to the list of conditions to automatically remove this alert (and raise some investigation alerts).

##### htn_diag_1

> if a patient has a hypertension diagnosis, they should also have a hypertension grade

grade is calculated from systolic blood pressure values.  In this artificial setup we indicate that the patient has hypertension but [omit blood pressure results](https://labs.openclinical.net/matt/dp_htn?conditions=["HTN"]) so that grade is missing.

#### investigations

#### referral

#### follow_up
