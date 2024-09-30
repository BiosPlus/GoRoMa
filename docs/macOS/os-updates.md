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


### Option One: The all-in-one (AIO) Nudge mobileconfig file

This works on the basis that you deploy a mobileconfig file macs with a full configuration. I apologise, I'd make this a collapsed section but it totally breaks the formatting.

<!-- ```xml
{% include_relative resources/nudge-macos.mobileconfig %}
``` -->

### Option Two: The web based Nudge configuration.

This works on the basis that you deploy a mobileconfig file macs telling them where the actual configuration source is hosted. In this case, on github as a raw file.

<!-- ```xml
{% include_relative resources/nudge-macos-web.mobileconfig %}
```

```json
{% include_relative resources/com.github.macadmins.Nudge.json %}
``` -->

## MacOS 14+ (Sonoma and newer)

