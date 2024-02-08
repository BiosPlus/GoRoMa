---
layout: default
title: Google Chrome - Managed Browser Settings
parent: Google Workspace
---
# Google Chrome - Managed Browser Settings
{: .no_toc }

A set of browser configurations which can be managed via the Google Workspace Admin Console (or Group Policy if you're brave enough)
{: .fs-6 .fw-300 }

A quick heads up, I refer to things as "Shortcodes" in here, though their actual name is "Preference Names".

---

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

### Browser Reporting

If you're managing a Google Workspace instance/tenancy, you'll want this turned on as it sends logs to your audit and investigation log tool. 3 hours is the fastest frequency.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Managed browser reporting | Enabled managed browser cloud reporting | CloudReportingEnabled | [Link](https://admin.google.com/ac/chrome/settings/user/details/cloud_reporting) |
| Managed browser reporting upload frequency | 3 hours | CloudReportingUploadFrequency | [Link](https://admin.google.com/ac/chrome/settings/user/details/cloud_reporting_upload_frequency_category_item) |

### Content

Better user experience.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Show "Always Open" checkbox in external protocol dialog | User may select "Always allow" to skip all future confirmation prompts | ExternalProtocolDialogShowAlwaysOpenCheckbox | [Link](https://admin.google.com/ac/chrome/settings/user/details/external_protocol_dialog_show_always_open_checkbox_category_item) |

### Chrome Updates

The goals here are simply:
- Get browsers to update within 24 hours of a release.
- Have Chrome check every 60 mins to see if there's an update.
- Use a friendly endpoint for checking (cacheable url).
- Don't bother users prior to 9:30, so they can get their morning meets done.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Configuration | Show notification recommending relaunch |  | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Time Period (hours) | 24 | RelaunchHeadsUpPeriod | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Initial quiet period (hours) | 1 | RelaunchNotification | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch window start time | 09:30 | RelaunchNotificationPeriod | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch window duration (minutes) | 720 | RelaunchWindow | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Auto-update check period (minutes) | 60 |  | [Link](https://admin.google.com/ac/chrome/settings/user/details/auto_update_check_period_minutes_field_new) |
| Cacheable URLs | Attempt to provide cache-friendly download URLs |  | [Link](https://admin.google.com/ac/chrome/settings/user/details/download_preference_field) |

### Remote Access

This is in aid of restricting possible avenues for scammers to get into user workstations. I imagine every org has a desired and standard means of conducting remote support.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Firewall Traversal | Disable firewall traversal | RemoteAccessHostFirewallTraversal| [Link](https://admin.google.com/ac/chrome/settings/user/details/remote_access_host_firewall_traversal_category_item) |
| Remote support connections | Prevent remote support connections | RemoteAccessHostAllowRemoteSupportConnections | [Link](https://admin.google.com/ac/chrome/settings/user/details/remote_access_host_allow_remote_support_connections_setting_group) |
| Enterprise remote support connections | Prevent remote support connections from enterprise admins | RemoteAccessHostAllowEnterpriseRemoteSupportConnections | [Link](https://admin.google.com/ac/chrome/settings/user/details/remote_access_host_allow_enterprise_remote_support_connections_setting_group) |

### Security

I believe that every org should have a centralised password solution (see: Bitwarden, 1Password, etc), hence it makes sense to reduce the chance of passwords stored in unknown locations.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Password Manager | Never allow the use of password manager | PasswordManagerEnabled | [Link](https://admin.google.com/ac/chrome/settings/user/details/password_manager) | 

### Other Settings

The logs that are sent are entirely anonymized and are extremely useful for helping the chromium team resolve issues. I believe there is value in turning this on if you're a workspace customer.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Metrics Reporting | Send anonymous reports of usage and crash-related data to Google | MetricsReportingEnabled | [Link](https://admin.google.com/ac/chrome/settings/user/details/metrics_reporting_enabled_category_item) |

### URL Blocking

This can be configured [here](https://admin.google.com/ac/chrome/settings/user/details/url_blocking_category_item), or via shortcode ```URLBlocklist```. 

{: .highlight}
This section is rather unique since it'll be a list of URLs rather than a single configurable option.

| URL | Reason |
|---|---|
| ```https://remotedesktop.google.com``` | Chromes Remote Desktop service (also needed to get `chromeRemoteDesktopAppBlocked` to equal `true` in the [device trust connector](chrome://connectors-internals/)) |
| ```https://remotedesktop.corp.google.com``` | Google Internal(?) Chrome Remote Desktop service (also needed to get `chromeRemoteDesktopAppBlocked` to equal `true` in the [device trust connector](chrome://connectors-internals/)) |