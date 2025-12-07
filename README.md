# 📱 EMA Client App – Research Deployment Guide

This mobile application is designed for **Ecological Momentary Assessment (EMA)** research studies.  
It enables researchers to:

- Configure complex EMA schedules
- Deploy Qualtrics, Google Forms, or custom web surveys
- Automatically detect participant survey submission
- Schedule local notifications on the participant’s device
- Prevent accidental exits and premature completion

This guide explains the **Complete Research Workflow** from configuration to deployment.

---

## ✅ 1. Create Your Study Using the EMA Configurator

Before using this mobile app, **you must first generate an EMA configuration file using the EMA Configurator**.

The configurator allows researchers to define:

- Project title and description
- EMA survey sequence
- Daily schedules and timing
- Notification behavior
- Editing lock rules (e.g. `allow_Edit`)

---

### 📄 Example EMA Configuration Output

Link: "https://regendchui.github.io/EMAapp/"
You should avoid using the sting "EMA_Index_Number_" in any field of EMA configurator.

```js
var contact_Person = "Dr Cheung";
var contact_Number = "12345678";
var project_Title = "My EMA";
var project_Description = "This is an EMA project";

var allow_Edit = true;
var close_Finish = true;
var display_Progress = true;

var EMA_Index_Number_1 = {
  start: 0,
  duration: 60000,
  label: "EMA 1",
  link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
  allow_Revert: true,
  allow_Discard: true,
  notification: [
    { content: "EMA 1 Noti 1", minutes: 0 },
    { content: "EMA 1 Noti 2", minutes: 3 }
  ],
  followUp: [
    {
      start: 0,
      duration: 60000,
      label: "EMA 1 FU 1",
      link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "EMA 1 FU 1 Noti 1", minutes: 0 },
        { content: "EMA 1 FU 1 Noti 2", minutes: 1 }
      ]
    },
    {
      start: 5,
      duration: 60000,
      label: "EMA 1 FU 2",
      link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "EMA 1 FU 2 Noti 1", minutes: 0 },
        { content: "EMA 1 FU 2 Noti 2", minutes: 1 }
      ]
    }
  ]
};

var EMA_Index_Number_2 = {
  start: 0,
  duration: 60000,
  label: "EMA 2",
  link: "https://hku.au1.qualtrics.com/jfe/form/SV_43fHbiTvotWDLPU",
  allow_Revert: true,
  allow_Discard: true,
  notification: [
    { content: "EMA 2 Noti 1", minutes: 0 },
    { content: "EMA 2 Noti 2", minutes: 3 }
  ],
  followUp: [
    {
      start: 0,
      duration: 60000,
      label: "EMA 2 FU 1",
      link: "https://hku.au1.qualtrics.com/jfe/form/SV_43fHbiTvotWDLPU",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "EMA 2 FU 1 Noti 1", minutes: 0 },
        { content: "EMA 2 FU 1 Noti 2", minutes: 1 }
      ]
    }
  ]
};

var EMA_Index_Number_3 = {
  start: 0,
  duration: 60000,
  label: "EMA 3",
  link: "https://village.derekslab.com/counselling/",
  allow_Revert: true,
  allow_Discard: true,
  notification: [
  ],
  followUp: [
  ]
};

var EMA_sequence = [EMA_Index_Number_1, EMA_Index_Number_2, EMA_Index_Number_3];

var Extra_Index_Number_1 = {
  start: 0,
  duration: 60000,
  label: "Extra 1",
  link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
  limit: 3,
  notification_Close_AfterTry: true,
  allow_Revert: true,
  allow_Discard: true,
  notification: [
    { content: "Extra 1 Noti 1", minutes: 0 },
    { content: "Extra 1 Noti 2", minutes: 3 }
  ],
  followUp: [
    {
      start: 0,
      duration: 60000,
      label: "Extra 1 FU 1",
      link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "Extra 1 FU 1 Noti 1", minutes: 0 },
        { content: "Extra 1 FU 1 Noti 2", minutes: 1 }
      ]
    },
    {
      start: 0,
      duration: 60000,
      label: "Extra 1 FU 2",
      link: "https://docs.google.com/forms/d/e/1FAIpQLSd9jHt-NWfCbzq0lgiGdKnfOlPOnPy38y0PDpVGZbBVoi9otQ/viewform",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "Extra 1 FU 1 Noti 1", minutes: 0 },
        { content: "Extra 1 FU 1 Noti 2", minutes: 1 }
      ]
    }
  ]
};

var Extra_Index_Number_2 = {
  start: 0,
  duration: 60000,
  label: "Extra 2",
  link: "https://hku.au1.qualtrics.com/jfe/form/SV_43fHbiTvotWDLPU",
  limit: 0,
  notification_Close_AfterTry: true,
  allow_Revert: true,
  allow_Discard: true,
  notification: [
    { content: "Extra 2 Noti 1", minutes: 0 },
    { content: "Extra 2 Noti 2", minutes: 3 }
  ],
  followUp: [
    {
      start: 0,
      duration: 60000,
      label: "Extra 2 FU 1",
      link: "https://hku.au1.qualtrics.com/jfe/form/SV_43fHbiTvotWDLPU",
      allow_Revert: true,
      allow_Discard: true,
      notification: [
        { content: "Extra 2 FU 1 Noti 1", minutes: 0 },
        { content: "Extra 2 FU 1 Noti 2", minutes: 1 }
      ]
    }
  ]
};

var Extra_Index_Number_3 = {
  start: 0,
  duration: 60000,
  label: "Extra 3",
  link: "https://village.derekslab.com/counselling/",
  limit: 1,
  notification_Close_AfterTry: true,
  allow_Revert: true,
  allow_Discard: true,
  notification: [
  ],
  followUp: [
  ]
};

var Extra_sequence = [Extra_Index_Number_1, Extra_Index_Number_2, Extra_Index_Number_3];


```

## ✅ 2. Load the Config File into the Client App

Once the EMA configuration is ready, researchers can load it into the app using three supported methods.

### 🔹 Method A — Paste Config Manually

  1. Open the Setup Screen

  2. Expand “Manage EMA Configuration”

  3. Paste the EMA configuration into the text box

  3. Tap “Parse Pasted Config”

✅ The app validates and loads immediately.

### 🔹 Method B — Upload Config File

  1. Open Manage EMA Configuration

  2. Tap “Upload EMA Config File”

  3. Select the config file from your device

✅ The app validates and loads immediately.


### 🔹Method C — Load Config from GitHub (Recommended ✅)

  1. Upload your config file to GitHub, Example: "https://raw.githubusercontent.com/user/EMAapp/refs/heads/main/ema-config-git.txt"

  2. Paste the GitHub link

  3. Tap “Preview from GitHub”
  
  4. Review project information
    
  5. Tap “Apply This GitHub Config”

✅ The app validates and loads immediately.

### 🔒 Configuration Locking

Once the Commencement Date is confirmed:

- Configuration editing is locked

- GitHub loading, uploading, and pasting are disabled

- Prevents accidental study corruption during data collection

## 📱 Automatic Survey Submission Detection

The app automatically detects survey completion across three supported platforms.
Once detected:

- ✅ EMA is marked as completed

Not detected:

- ✅ When user close the web view, it will ask client to mark the EMA as finished if they have finished the EMA.

### ✅ Qualtrics Auto-Detection

The app detects submission when any of the following exists on the webpage:
  - #EndOfSurvey
  - .EndOfSurvey
  - [class*="EndOfSurvey"]

✅ Works with:
- Default Qualtrics ending pages
- Custom end-of-survey messages

### ✅ Google Forms Auto-Detection

Google Forms is detected using the redirect URL pattern:
- /formResponse
- Example: https://docs.google.com/forms/d/e/xxxxx/formResponse

### ✅ Wordpress plugin - Formidable Auto-Detection

If using a Wordpress website with formidable as survey agent, detection triggers when this element exists:
- <div class="frm_message"></div>

## 📱 WebView Cache Control

The app allows clients to clear WebView cache:

1. Open any EMA survey
2. Tap “Clear” in the top-right corner
3. Confirm cache reset
4. WebView reloads cleanly

If you use Wordpress as survey agent, users can stay login after cleaning cache as long as the login session is not expired.


## 📄 Recommended Research Workflow
1. Design your EMA study using the EMA Configurator
2. Export and upload the config file to GitHub
3. Participants install the mobile app
4. Participants load the GitHub config
5. Participants confirm commencement date


## ✅ The app automatically handles:
- Notification scheduling

- EMA deployment

- Survey completion detection

- Completion tracking
