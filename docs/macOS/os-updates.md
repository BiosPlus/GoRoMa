---
layout: default
title: MacOS Updates
parent: macOS
---

# MacOS Updates
{: .no_toc }

My best practice methodology for MacOS software (OS) updates.
{: .fs-6 .fw-300 }

---


## Pre MacOS 14 (Ventura and older)

MacOS versions pre-sonoma lacked a good update workflow methodology, this is because Apple designs things in a way where actions are user driven first, automatic second. Therefore while MDMs could attempt to enforce an update schedule, the actual kickoff to drive the update process always needed to be driven by the user.

The best approach to combat this is to use Nudge.
- Deploy the Nudge Suite package from the macadmins github release page ([Link](https://github.com/macadmins/nudge/releases))
    - Keep in mind, deploy this to a device group in your MDM where you can set a conditional rule wherin the OS version is older than 14.0 for application.
- Create a policy to enforce updates via Nudge, or use my existing web JSON based policy. Both are listed below (as of 2024-01-31):

```filename: nudge-macos.mobileconfig```

{% capture nudge_mobileconfig %}
{% include_relative resources/nudge-macos.mobileconfig %}
{% endcapture %}

<details>
    <summary>Click to expand/collapse codeblock</summary>
    ```xml
    {{ nudge_mobileconfig }}```
</details>

{% capture nudge_mobileconfig_web %}
{% include_relative resources/nudge-macos-web.mobileconfig %}
{% endcapture %}

```filename: nudge-macos-web.mobileconfig```

<details>
    <summary>Click to expand/collapse codeblock</summary>
    ```xml
    {{ nudge_mobileconfig_web }}```
</details>

## MacOS 14+ (Sonoma and newer)

