---
layout: default
title: Managed Browser Settings
parent: Google Chrome
grand_parent: Google Workspace
---
# Managed Browser Settings
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
| Event Reporting | Enable event reporting | OnSecurityEventEnterpriseConnector | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnSecurityEventEnterpriseConnector&table-view=false) |

### Chrome Enterprise Connectors

- Hashes are generated for uploaded/downloaded files
- Huge text pastes are analysed for potential PII exfiltration.
- Visits to malicious URLs (w/ the red advisory block screen) are logged + graded on severity.
    - Bypasses of that advisory are logged and reported.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Upload content analysis | [More info to come] | OnFileAttachedEnterpriseConnector | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnFileAttachedEnterpriseConnector&table-view=false) |
| Download content analysis | [More info to come] | OnFileDownloadedEnterpriseConnector | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnFileDownloadedEnterpriseConnector&table-view=false) |
| Bulk text content analysis | [More info to come] | OnBulkDataEntryEnterpriseConnector | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnBulkDataEntryEnterpriseConnector&table-view=false) |
| Print content analysis | [More info to come] | OnPrintEnterpriseConnector | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnPrintEnterpriseConnector&table-view=false) |
| Real time URL check | Chrome Enterprise Premium | EnterpriseRealTimeUrlCheckMode | [Link](https://admin.google.com/ac/chrome/settings/user?ref=browser&f=POLICY_NAME.OnFileDownloadedEnterpriseConnector&table-view=false) |

### Chrome Updates

The goals here are simply:
- Get browsers to update within 48 hours of a release.
- Have Chrome check every 300 mins to see if there's an update.
- Use a friendly endpoint for checking (cacheable url).
- Use the extended stable channel for stability and due to the amount of updates the chrome team tend to push a day on the latest channel in comparison (Sometimes several times a day on latest).

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Relaunch notificaiton: Configuration | Show notification recommending relaunch | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch notificaiton: Time Period (hours) | 48 | RelaunchHeadsUpPeriod | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch notificaiton: Initial quiet period (hours) | 4 | RelaunchNotification | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch notificaiton: Relaunch window start time | 00:00 | RelaunchNotificationPeriod | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Relaunch notificaiton: Relaunch window duration (minutes) | 1440 | RelaunchWindow | [Link](https://admin.google.com/ac/chrome/settings/user/details/relaunch_notification_with_duration) |
| Auto-update check period (minutes) | 300 | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/auto_update_check_period_minutes_field_new) |
| Cacheable URLs | Attempt to provide cache-friendly download URLs | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/download_preference_field) |
| Google updater policy precedence | Cloud Google Updater policy override platform policy | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/omaha_policy_precedence_category_item) |
| Supress auto-update check: Start Time | 08:30 | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/updates_suppressed) |
| Supress auto-update check: Duration (minutes) | 120 | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/updates_suppressed) |
| Chrome browser updates: Configuration | Allow updates | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/chrome_browser_updates) |
| Chrome browser updates: Channel | Extended stable channel | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/chrome_browser_updates) |


### Content

Better user experience.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Show "Always Open" checkbox in external protocol dialog | User may select "Always allow" to skip all future confirmation prompts | ExternalProtocolDialogShowAlwaysOpenCheckbox | [Link](https://admin.google.com/ac/chrome/settings/user/details/external_protocol_dialog_show_always_open_checkbox_category_item) |

### Enrollment controls

Populating data about the devices joining your org.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Asset identifier during enrollment | Users in this organization can procide asset ID and location during enrollment | ??? | [Link](https://admin.google.com/ac/chrome/settings/user/details/allow_populate_asset_identifier) |

### Import Settings

Right now this pertains to password imports, the password manager isn't working (if you follow the rule a few sections below this) but this is a good step to take anyway.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Import saved passwords | Disable import of saved passwords | ImportSavedPasswords | [Link](https://admin.google.com/ac/chrome/settings/user/details/import_saved_passwords_category_item) | 


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

### Sign-In Settings

This is in aid of securing your data and ensuring that users are not syncing things like history or bookmarks or passwords to a personal gmail account.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Browser sign-in settings | Enable browser sign-in | BrowserSignin | [Link](https://admin.google.com/ac/chrome/settings/user/details/browser_signin_category_item) | 
| Separate profile for managed Google Identity | Force seperate profile and forbit secondary managed accounts | ManagedAccountsSigninRestriction | [Link](https://admin.google.com/ac/chrome/settings/user/details/managed_accounts_signin_restriction_category_item) | 
| Enterprise profile separation | Enforce profile seperation | ProfileSeparationSettings | [Link](https://admin.google.com/ac/chrome/settings/user/details/profile_separation_settings_setting_group) | 
| Profile seperation data migration | Suggest to users to bring their existing data in the managed profile and give them a choice not to | ProfileSeparationDataMigrationSettings | [Link](https://admin.google.com/ac/chrome/settings/user/details/profile_separation_data_migration_settings_setting_group) | 


### Other Settings

The logs that are sent are entirely anonymized and are extremely useful for helping the chromium team resolve issues. I believe there is value in turning this on if you're a workspace customer.
Policy fetching is set to 300 in the event you push a bad config and realise your mistake + want to rollback before anyone gets it.
Backing up chrome data locally is a general no-no.

| Policy | Setting | Shortcode | <span style="display: inline-block; max-width:100px">URL</span> |
|---|-----|----------|:-:|
| Metrics Reporting | Send anonymous reports of usage and crash-related data to Google | MetricsReportingEnabled | [Link](https://admin.google.com/ac/chrome/settings/user/details/metrics_reporting_enabled_category_item) |
| Policy fetch delay | 300 seconds | MaxInvalidationFetchDelay | [Link](https://admin.google.com/ac/chrome/settings/user/details/max_invalidation_fetch_delay_category_item) |
| Backup of Google Chrome data | Prevent Google Chrome data from being included in backups | AllowChromeDataInBackups | [Link](https://admin.google.com/ac/chrome/settings/user/details/allow_chrome_data_in_backups_setting_group) |

### URL Blocking

This can be configured [here](https://admin.google.com/ac/chrome/settings/user/details/url_blocking_category_item), or via shortcode ```URLBlocklist```. 

{: .highlight}
This section is rather unique since it'll be a list of URLs rather than a single configurable option.

| URL | Reason |
|---|---|
| ```https://remotedesktop.google.com``` | Chromes Remote Desktop service (needed to get `chromeRemoteDesktopAppBlocked` to equal `true` in the [device trust connector](chrome://connectors-internals/)) |
| ```https://remotedesktop.corp.google.com``` | Google Internal(?) Chrome Remote Desktop service (also needed to get `chromeRemoteDesktopAppBlocked` to equal `true` in the [device trust connector](chrome://connectors-internals/)) |