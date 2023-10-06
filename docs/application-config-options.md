# Application Configuration Options for the OneDrive Client for Linux
## Application Version
Before reading this document, please ensure you are running application version [![Version](https://img.shields.io/github/v/release/abraunegg/onedrive)](https://github.com/abraunegg/onedrive/releases) or greater. Use `onedrive --version` to determine what application version you are using and upgrade your client if required.

## Table of Contents
TABLE OF CONTENTS GOES HERE

## Configuration File Options

### application_id
_**Description:**_ This is the config option for application id that used used to identify itself to Microsoft OneDrive. In some circumstances, it may be desirable to use your own application id. To do this, you must register a new application with Microsoft Azure via	https://portal.azure.com/, then use your new application id with this config option.

_**Value Type:**_ String

_**Default Value:**_ d50ca740-c83f-4d1b-b616-12c519384f0c

_**Config Example:**_ `application_id = "d50ca740-c83f-4d1b-b616-12c519384f0c"`

### azure_ad_endpoint
_**Description:**_ This is the config option to change the Microsoft Azure Authentication Endpoint that the client uses to conform with data and security requirements that requires data to reside within the geographic borders of that country.

_**Value Type:**_ String

_**Default Value:**_ *Empty* - not required for normal operation

_**Valid Values:**_ USL4, USL5, DE, CN

_**Config Example:**_ `azure_ad_endpoint = "DE"`

### azure_tenant_id
_**Description:**_ This config option allows the locking of the client to a specific single tenant and will configure your client to use the specified tenant id in its Azure AD and Graph endpoint URIs, instead of "common". The tenant id may be the GUID Directory ID or the fully qualified tenant name.

_**Value Type:**_ String

_**Default Value:**_ *Empty* - not required for normal operation

_**Config Example:**_ `azure_tenant_id = "example.onmicrosoft.us"` or `azure_tenant_id = "0c4be462-a1ab-499b-99e0-da08ce52a2cc"`

_**Additional Usage Requirement:**_ Must be configured if 'azure_ad_endpoint' is configured.

### bypass_data_preservation
_**Description:**_ This config option allows the disabling of preserving local data by renaming the local file in the event of data conflict. If this is enabled, you will experience data loss on your local data as the local file will be over-written with data from OneDrive online. Use with care and caution.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `bypass_data_preservation = "false"` or `bypass_data_preservation = "true"`

### check_nomount
_**Description:**_ This config option is useful to prevent application startup & ongoing use in 'Monitor Mode' if the configured 'sync_dir' is a separate disk that is being mounted by your system. This option will check for the presence of a `.nosync` file in your mount point, and if present, abort any sync process to preserve data.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `check_nomount = "false"` or `check_nomount = "true"`

_**CLI Option:**_ `--check-for-nomount`

_**Additional Usage Requirement:**_ Create a `.nosync` file in your mount point *before* you mount your disk so that this is visible, in your mount point if your disk is unmounted.

### check_nosync
_**Description:**_ This config option is useful to prevent the sync of a *local* directory to Microsoft OneDrive. It will *not* check for this file online to prevent the download of directories to your local system.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `check_nosync = "false"` or `check_nosync = "true"`

_**CLI Option Use:**_ `--check-for-nosync`

_**Additional Usage Requirement:**_ Create a `.nosync` file in any *local* directory that you wish to not sync to Microsoft OneDrive when you enable this option.

### classify_as_big_delete
_**Description:**_ This config option defines the number of children in a path that is locally removed which will be classified as a 'big data delete' to safeguard large data removals - which are typically accidental local delete events.

_**Value Type:**_ Integer

_**Default Value:**_ 1000

_**Config Example:**_ `classify_as_big_delete = "2000"`

_**CLI Option Use:**_ `--classify-as-big-delete 2000`

_**Additional Usage Requirement:**_ If this option is triggered, you will need to add `--force` to force a sync to occur.

### cleanup_local_files
_**Description:**_ This config option provides the capability to cleanup local files and folders if they are removed online.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `cleanup_local_files = "false"` or `cleanup_local_files = "true"`

_**CLI Option Use:**_ `--cleanup-local-files`

_**Additional Usage Requirement:**_ This configuration option can only be used with 'download_only'. It cannot be used with any other application option.

### connect_timeout
_**Description:**_ This configuration setting manages the TCP connection timeout duration in seconds for HTTPS connections to Microsoft OneDrive when using the curl library.

_**Value Type:**_ Integer

_**Default Value:**_ 30

_**Config Example:**_ `connect_timeout = "20"`

### data_timeout
_**Description:**_ This setting controls the timeout duration, in seconds, for when data is not received on an active connection to Microsoft OneDrive over HTTPS when using the curl library, before that connection is timeout out.

_**Value Type:**_ Integer

_**Default Value:**_ 240

_**Config Example:**_ `data_timeout = "300"`

### debug_https
_**Description:**_ This setting controls whether the curl library is configured to output additional data to assist with diagnosing HTTPS issues and problems.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `debug_https = "false"` or `debug_https = "true"`

_**CLI Option Use:**_ `--debug-https`

_**Additional Usage Notes:**_ Whilst this option can be used at any time, it is advisable that you only use this option when advised as this will output your `Authorization: bearer` - which is your authentication token to Microsoft OneDrive.

### disable_download_validation
_**Description:**_ This option determines whether the client will conduct integrity validation on files downloaded from Microsoft OneDrive. Sometimes, when downloading files, particularly from SharePoint, there is a discrepancy between the file size reported by the OneDrive API and the byte count received from the SharePoint HTTP Server for the same file. Enable this option to disable the integrity checks performed by this client.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `disable_download_validation = "false"` or `disable_download_validation = "true"`

_**CLI Option Use:**_ `--disable-download-validation`

_**Additional Usage Notes:**_ If you're downloading data from SharePoint or OneDrive Business Shared Folders, you might find it necessary to activate this option. It's important to note that any issues encountered aren't due to a problem with this client; instead, they should be regarded as issues with the Microsoft OneDrive technology stack.

### disable_notifications
_**Description:**_ This setting controls whether GUI notifications are sent from the client to your display manager session. 

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `disable_notifications = "false"` or `disable_notifications = "true"`

_**CLI Option Use:**_ `--disable-notifications`

### disable_upload_validation
_**Description:**_ This option determines whether the client will conduct integrity validation on files uploaded to Microsoft OneDrive. Sometimes, when uploading files, particularly to SharePoint, SharePoint will modify your file post upload by adding new data to your file which breaks the integrity checking of the upload performed by this client. Enable this option to disable the integrity checks performed by this client.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `disable_upload_validation = "false"` or `disable_upload_validation = "true"`

_**CLI Option Use:**_ `--disable-upload-validation`

_**Additional Usage Notes:**_ If you're uploading data to SharePoint or OneDrive Business Shared Folders, you might find it necessary to activate this option. It's important to note that any issues encountered aren't due to a problem with this client; instead, they should be regarded as issues with the Microsoft OneDrive technology stack.

### display_running_config
_**Description:**_ This option will include the running config of the application at application startup. This may be desirable to enable when running in containerised environments so that any application logging that is occuring, will have the application configuration being consumed at startup, written out to any applicable log file.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `display_running_config = "false"` or `display_running_config = "true"`

_**CLI Option Use:**_ `--display-running-config`

### dns_timeout
_**Description:**_ This setting controls the libcurl DNS cache value. By default, libcurl caches this info for 60 seconds. This libcurl DNS cache timeout is entirely speculative that a name resolves to the same address for a small amount of time into the future as libcurl does not use DNS TTL properties. We recommend users not to tamper with this option unless strictly necessary.

_**Value Type:**_ Integer

_**Default Value:**_ 60

_**Config Example:**_ `dns_timeout = "90"`

### download_only
_**Description:**_ This setting forces the client to only download data from Microsoft OneDrive and replicate that data locally. No changes made locally will be uploaded to Microsoft OneDrive when using this option.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `download_only = "false"` or `download_only = "true"`

_**CLI Option Use:**_ `--download-only`

### drive_id
_**Description:**_ This setting controls the specific drive identifier the client will use when syncing with Microsoft OneDrive.

_**Value Type:**_ String

_**Default Value:**_ *None*

_**Config Example:**_ `drive_id = "b!bO8V6s9SSk9R7mWhpIjUrotN73WlW3tEv3OxP_QfIdQimEdOHR-1So6CqeG1MfDB"`

_**Additional Usage Notes:**_ This option is typically only used when configuring the client to sync a specific SharePoint Library. If this configuration option is specified in your config file, a value must be specified otherwise the application will exit citing a fatal error has occured.

### dry_run
_**Description:**_ This setting controls the application capability to test your application configuration without actually performing any actual activity (download, upload, move, delete, folder creation).

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `dry_run = "false"` or `dry_run = "true"`

_**CLI Option Use:**_ `--dry-run`

### enable_logging
_**Description:**_ This setting controls the application logging all actions to a separate file. By default, all log files will be written to `/var/log/onedrive`, however this can changed by using the 'log_dir' config option

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `enable_logging = "false"` or `enable_logging = "true"`

_**CLI Option Use:**_ `--enable-logging`

_**Additional Usage Notes:**_ Additional configuration is potentially required to configure the default log directory. Refer to usage.md for details (ADD LINK)

### force_http_11
_**Description:**_ This setting controls the application HTTP protocol version. By default, the application will use libcurl defaults for which HTTP prodocol version will be used to interact with Microsoft OneDrive. Use this setting to downgrade libcurl to only use HTTP/1.1.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `force_http_11 = "false"` or `force_http_11 = "true"`

_**CLI Option Use:**_ `--force-http-11`

### ip_protocol_version
_**Description:**_ This setting controls the application IP protocol that should be used when communicating with Microsoft OneDrive. The default is to use IPv4 and IPv6 networks for communicating to Microsoft OneDrive.

_**Value Type:**_ Integer

_**Default Value:**_ 0

_**Valid Values:**_ 0 = IPv4 + IPv6, 1 = IPv4 Only, 2 = IPv6 Only

_**Config Example:**_ `ip_protocol_version = "0"` or `ip_protocol_version = "1"` or `ip_protocol_version = "2"`

_**Additional Usage Notes:**_ In some environments where IPv4 and IPv6 are configured at the same time, this causes resolution and routing issues to Microsoft OneDrive. If this is the case, it is advisable to change 'ip_protocol_version' to match your environment.

### local_first
_**Description:**_ This setting controls what the application considers the 'source of truth' for your data. By default, what is stored online will be considered as the 'source of truth' when syncing to your local machine. When using this option, your local data will be considered the 'source of truth'.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `local_first = "false"` or `local_first = "true"`

_**CLI Option Use:**_ `--local-first`

### log_dir
_**Description:**_ This setting controls the custom application log path when 'enable_logging' has been enabled. By default, all log files will be written to `/var/log/onedrive`.

_**Value Type:**_ String

_**Default Value:**_ *None*

_**Config Example:**_ `log_dir = "~/logs/"`

_**CLI Option Use:**_ `--log-dir "~/logs/"`

### monitor_fullscan_frequency
_**Description:**_ This configuration option controls the number of 'monitor_interval' iterations between when a full scan of your data is performed to ensure data integrity and consistency.

_**Value Type:**_ Integer

_**Default Value:**_ 12

_**Config Example:**_ `monitor_fullscan_frequency = "24"`

_**CLI Option Use:**_ `--monitor-fullscan-frequency '24'`

_**Additional Usage Notes:**_ By default without configuration, 'monitor_fullscan_frequency' is set to 12. In this default state, this means that a full scan is performed every 'monitor_interval' x 'monitor_fullscan_frequency' = 3600 seconds. This setting is only applicable when running in `--monitor` mode.

### monitor_interval
_**Description:**_ This configuration setting determines how often the synchronisation loops run in --monitor mode, measured in seconds. When this time period elapses, the client will check for online changes in Microsoft OneDrive, conduct integrity checks on local data and scan the local 'sync_dir' to identify any new content that hasn't been uploaded yet.

_**Value Type:**_ Integer

_**Default Value:**_ 300

_**Config Example:**_ `monitor_interval = "600"`

_**CLI Option Use:**_ `--monitor-interval '600'`

_**Additional Usage Notes:**_ A minimum value of 300 is enforced for this configuration setting.

### monitor_log_frequency
_**Description:**_ This configuration option controls the suppression of frequently printed log items to the system console when using `--monitor` mode. The aim of this configuration item is to reduce the log output when near zero sync activity is occuring.

_**Value Type:**_ Integer

_**Default Value:**_ 12

_**Config Example:**_ `monitor_log_frequency = "24"`

_**CLI Option Use:**_ `--monitor-log-frequency '24'`

_**Additional Usage Notes:**_ 

By default, at application start-up when using `--monitor` mode, the following will be logged to indicate that the application has correctly started and has performed all the initial processing steps:
```text
Reading configuration file: /home/user/.config/onedrive/config
Configuration file successfully loaded
Configuring Global Azure AD Endpoints
Sync Engine Initialised with new Onedrive API instance
All application operations will be performed in: /home/user/OneDrive
OneDrive synchronisation interval (seconds): 300
Initialising filesystem inotify monitoring ...
Performing initial syncronisation to ensure consistent local state ...
Starting a sync with Microsoft OneDrive
Fetching items from the OneDrive API for Drive ID: b!bO8V6s9SSk9R7mWhpIjUrotN73WlW3tEv3OxP_QfIdQimEdOHR-1So6CqeG1MfDB ..
Processing changes and items received from Microsoft OneDrive ...
Performing a database consistency and integrity check on locally stored data ... 
Scanning the local file system '~/OneDrive' for new data to upload ...
Performing a final true-up scan of online data from Microsoft OneDrive
Fetching items from the OneDrive API for Drive ID: b!bO8V6s9SSk9R7mWhpIjUrotN73WlW3tEv3OxP_QfIdQimEdOHR-1So6CqeG1MfDB ..
Processing changes and items received from Microsoft OneDrive ...
Sync with Microsoft OneDrive is complete
```
Then, based on 'monitor_log_frequency', the following output will be logged until the suppression loop value is reached:
```text
Starting a sync with Microsoft OneDrive
Syncing changes from Microsoft OneDrive ...
Sync with Microsoft OneDrive is complete
```
**Note:** The additional log output `Performing a database consistency and integrity check on locally stored data ...` will only be displayed when this activity is occuring which is triggered by 'monitor_fullscan_frequency'.

**Note:** If verbose application output is being used (`--verbose`), then this configuration setting has zero effect, as application verbose output takes priority over application output surpression.

### no_remote_delete
_**Description:**_ This configuration option controls whether local file and folder deletes are actioned on Microsoft OneDrive.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `local_first = "false"` or `local_first = "true"`

_**CLI Option Use:**_ `--no-remote-delete`

_**Additional Usage Notes:**_ This configuration option can *only* be used in conjunction with `--upload-only`

### operation_timeout
_**Description:**_ This configuration option controls the maximum amount of time (seconds) a file operation is allowed to take. This includes DNS resolution, connecting, data transfer, etc. We recommend users not to tamper with this option unless strictly necessary.

_**Value Type:**_ Integer

_**Default Value:**_ 3600

_**Config Example:**_ `operation_timeout = "3600"`

### rate_limit
_**Description:**_ This configuration option controls the bandwidth used by the application, per thread, when interacting with Microsoft OneDrive.

_**Value Type:**_ Integer

_**Default Value:**_ 0 (unlimited, use available bandwidth per thread)

_**Valid Values:**_ Valid tested values for this configuration option are as follows:

* 131072 	= 128 KB/s - absolute minimum for basic application operations to prevent timeouts
* 262144 	= 256 KB/s
* 524288	= 512 KB/s
* 1048576 	= 1 MB/s
* 10485760 	= 10 MB/s
* 104857600 = 100 MB/s

_**Config Example:**_ `rate_limit = "131072"`

### read_only_auth_scope
_**Description:**_ This configuration option controls whether the OneDrive Client for Linux operates in a totally in read-only operation.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `read_only_auth_scope = "false"` or `read_only_auth_scope = "true"`

_**Additional Usage Notes:**_ When using 'read_only_auth_scope' you also will need to remove your existing application access consent otherwise old authentication consent will be valid and will be used. This will mean the application will technically have the consent to upload data until you revoke this consent.

### remove_source_files
_**Description:**_ This configuration option controls whether the OneDrive Client for Linux removes the local file post successful transfer to Microsoft OneDrive.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `remove_source_files = "false"` or `remove_source_files = "true"`

_**CLI Option Use:**_ `--remove-source-files`

_**Additional Usage Notes:**_ This configuration option can *only* be used in conjunction with `--upload-only`

### resync
_**Description:**_ This configuration option controls whether the known local sync state with Microsoft OneDrive is removed at application startup. When this option is used, a full scan of your data online is performed to ensure that the local sync state is correctly built back up.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `resync = "false"` or `resync = "true"`

_**CLI Option Use:**_ `--resync`

_**Additional Usage Notes:**_ It's highly recommended to use this option only if the application prompts you to do so. Don't blindly use this option as a default option. If you alter any of the subsequent configuration items, you will be required to execute a `--resync` to make sure your client is syncing your data with the updated configuration:
*   drive_id
*   sync_dir
*   skip_file
*   skip_dir
*   skip_dotfiles
*   skip_symlinks
*   sync_business_shared_items
*   Creating, Modifying or Deleting the 'sync_list' file

### resync_auth
_**Description:**_ This configuration option controls the approval of performing a 'resync' which can be beneficial in automated environments.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `resync_auth = "false"` or `resync_auth = "true"`

_**CLI Option Use:**_ `--resync-auth`

_**Additional Usage Notes:**_ In certain automated environments (assuming you know what you're doing due to automation), to avoid the 'proceed with acknowledgement' resync requirement, this option allows you to automatically acknowledge the resync prompt.

### skip_dir
_**Description:**_ This configuration option controls whether the application skips certain directories from being synced.

_**Value Type:**_ String

_**Default Value:**_ *Empty* - not required for normal operation

_**Config Example:**_ 

Patterns are case insensitive. `*` and `?` [wildcards characters](https://technet.microsoft.com/en-us/library/bb490639.aspx) are supported. Use `|` to separate multiple patterns. Entries for 'skip_dir' are *relative* to your 'sync_dir' path.
```text
# When changing a config option below, remove the '#' from the start of the line
# For explanations of all config options below see docs/USAGE.md or the man page.
#
# sync_dir = "~/OneDrive"
# skip_file = "~*|.~*|*.tmp"
# monitor_interval = "300"
skip_dir = "Desktop|Documents/IISExpress|Documents/SQL Server Management Studio|Documents/Visual Studio*|Documents/WindowsPowerShell"
# log_dir = "/var/log/onedrive/"
```

The 'skip_dir' option can be specified multiple times within your config file, for example:
```text
skip_dir = "SomeDir|OtherDir|ThisDir|ThatDir"
skip_dir = "/Path/To/A/Directory"
skip_dir = "/Another/Path/To/Different/Directory"
```

This will be interpreted the same as:
```text
skip_dir = "SomeDir|OtherDir|ThisDir|ThatDir|/Path/To/A/Directory|/Another/Path/To/Different/Directory"
```

_**CLI Option Use:**_ `--skip-dir 'SomeDir|OtherDir|ThisDir|ThatDir|/Path/To/A/Directory|/Another/Path/To/Different/Directory'`

_**Additional Usage Notes:**_ This option is considered a 'Client Side Filtering Rule' and if configured, is utilised for all sync operations. If using the config file and CLI option is used, the CLI option will *replace* the config file entries. After changing or modifying this option, you will be required to perform a resync.

### skip_dir_strict_match
_**Description:**_ This configuration option controls whether the application performs strict directory matching when checking 'skip_dir' items. When enabled, the 'skip_dir' item must be a full path match to the path to be skipped.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `skip_dir_strict_match = "false"` or `skip_dir_strict_match = "true"`

_**CLI Option Use:**_ `--skip-dir-strict-match`

### skip_dotfiles
_**Description:**_ This configuration option controls whether the application will skip all .files and .folders when performing sync operations.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `skip_dotfiles = "false"` or `skip_dotfiles = "true"`

_**CLI Option Use:**_ `--skip-dot-files`

_**Additional Usage Notes:**_ This option is considered a 'Client Side Filtering Rule' and if configured, is utilised for all sync operations. After changing this option, you will be required to perform a resync.

### skip_file
_**Description:**_ This configuration option controls whether the application skips certain files from being synced.

_**Value Type:**_ String

_**Default Value:**_ `~*|.~*|*.tmp|*.swp|*.partial`

_**Config Example:**_ 

Patterns are case insensitive. `*` and `?` [wildcards characters](https://technet.microsoft.com/en-us/library/bb490639.aspx) are supported. Use `|` to separate multiple patterns.

By default, the following files will be skipped:
*   Files that start with ~
*   Files that start with .~ (like .~lock.* files generated by LibreOffice)
*   Files that end in .tmp, .swp and .partial

Files can be skipped in the following fashion:
*   Specify a wildcard, eg: '*.txt' (skip all txt files)
*   Explicitly specify the filename and it's full path relative to your sync_dir, eg: '/path/to/file/filename.ext'
*   Explicitly specify the filename only and skip every instance of this filename, eg: 'filename.ext'

```text
# When changing a config option below, remove the '#' from the start of the line
# For explanations of all config options below see docs/USAGE.md or the man page.
#
# sync_dir = "~/OneDrive"
skip_file = "~*|/Documents/OneNote*|/Documents/config.xlaunch|myfile.ext|/Documents/keepass.kdbx"
# monitor_interval = "300"
# skip_dir = ""
# log_dir = "/var/log/onedrive/"
```
The 'skip_file' option can be specified multiple times within your config file, for example:
```text
skip_file = "~*|.~*|*.tmp|*.swp"
skip_file = "*.blah"
skip_file = "never_sync.file"
skip_file = "/Documents/keepass.kdbx"
```
This will be interpreted the same as:
```text
skip_file = "~*|.~*|*.tmp|*.swp|*.blah|never_sync.file|/Documents/keepass.kdbx"
```

_**CLI Option Use:**_ `--skip-file '~*|.~*|*.tmp|*.swp|*.blah|never_sync.file|/Documents/keepass.kdbx'`

_**Additional Usage Notes:**_ This option is considered a 'Client Side Filtering Rule' and if configured, is utilised for all sync operations. If using the config file and CLI option is used, the CLI option will *replace* the config file entries. After changing or modifying this option, you will be required to perform a resync.

### skip_size
_**Description:**_ This configuration option controls whether the application skips syncing certain files larger than the specified size. The value specified is in MB.

_**Value Type:**_ Integer

_**Default Value:**_ 0 (all files, regardless of size, are synced)

_**Config Example:**_ `skip_size = "50"`

_**CLI Option Use:**_ `--skip-size '50'`

### skip_symlinks
_**Description:**_ This configuration option controls whether the application will skip all symbolic links when performing sync operations. Microsoft OneDrive has no concept or understanding of symbolic links, and attempting to upload a symbolic link to Microsoft OneDrive generates a platform API error. All data (files and folders) that are uploaded to OneDrive must be whole files or actual directories.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `skip_symlinks = "false"` or `skip_symlinks = "true"`

_**CLI Option Use:**_ `--skip-symlinks`

_**Additional Usage Notes:**_ This option is considered a 'Client Side Filtering Rule' and if configured, is utilised for all sync operations. After changing this option, you will be required to perform a resync.

### space_reservation
_**Description:**_ This configuration option controls how much local disk space should be reserved, to prevent the application from filling up your entire disk due to misconfiguration

_**Value Type:**_ Integer

_**Default Value:**_ 50 MB (expressesed as Bytes when using `--display-config`)

_**Config Example:**_ `space_reservation = "100"`

_**CLI Option Use:**_ `--space-reservation '100'`

### sync_business_shared_items
_**Description:**_ This configuration option controls whether OneDrive Business | Office 365 Shared Folders, when added as a 'shortcut' to your 'My Files' will be synced to your local system.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `sync_business_shared_items = "false"` or `sync_business_shared_items = "true"`

_**CLI Option Use:**_ *none* - this is a config file option only

_**Additional Usage Notes:**_ This option is considered a 'Client Side Filtering Rule' and if configured, is utilised for all sync operations. After changing this option, you will be required to perform a resync.

### sync_dir
_**Description:**_ This configuration option determines the location on your local filesystem where your data from Microsoft OneDrive will be saved.

_**Value Type:**_ String

_**Default Value:**_ `~/OneDrive`

_**Config Example:**_ `sync_dir = "~/MyDirToSync"`

_**CLI Option Use:**_ `--syncdir '~/MyDirToSync'`

_**Additional Usage Notes:**_ After changing this option, you will be required to perform a resync.

### sync_dir_permissions
_**Description:**_ This configuration option defines the directory permissions applied when a new directory is created locally during the process of syncing your data from Microsoft OneDrive.

_**Value Type:**_ Integer

_**Default Value:**_ `700` - This provides the following permissions: `drwx------`

_**Config Example:**_ `sync_dir_permissions = "700"`

_**Additional Usage Notes:**_ Use the [Unix Permissions Calculator](https://chmod-calculator.com/) to help you determine the necessary new permissions. You will need to manually update all existing directory permissions if you modify this value.

### sync_file_permissions
_**Description:**_ This configuration option defines the file permissions applied when a new file is created locally during the process of syncing your data from Microsoft OneDrive.

_**Value Type:**_ Integer

_**Default Value:**_ `600` - This provides the following permissions: `-rw-------`

_**Config Example:**_ `sync_file_permissions = "600"`

_**Additional Usage Notes:**_ Use the [Unix Permissions Calculator](https://chmod-calculator.com/) to help you determine the necessary new permissions. You will need to manually update all existing directory permissions if you modify this value.

### sync_root_files
_**Description:**_ This configuration option manages the synchronisation of files located in the 'sync_dir' root when using a 'sync_list.' It enables you to sync all these files by default, eliminating the need to repeatedly modify your 'sync_list' and initiate resynchronisation.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `sync_root_files = "false"` or `sync_root_files = "true"`

_**CLI Option Use:**_ `--sync-root-files`

_**Additional Usage Notes:**_ Although it's not mandatory, it's recommended that after enabling this option, you perform a `--resync`. This ensures that any previously excluded content is now included in your sync process.

### upload_only
_**Description:**_ This setting forces the client to only upload data to Microsoft OneDrive and replicate the locate state online. By default, this will also remove content online, that has been removed locally.

_**Value Type:**_ Boolean

_**Default Value:**_ False

_**Config Example:**_ `upload_only = "false"` or `upload_only = "true"`

_**CLI Option Use:**_ `--upload-only`

_**Additional Usage Notes:**_ To ensure that data deleted locally remains accessible online, you can use the 'no_remote_delete' option. If you want to delete the data from your local storage after a successful upload to Microsoft OneDrive, you can use the 'remove_source_files' option.

### user_agent
_**Description:**_ This configuration option controls the 'User-Agent' request header that is presented to Microsoft Graph API when accessing the Microsoft OneDrive service. This string lets servers and network peers identify the application, operating system, vendor, and/or version of the application making the request. We recommend users not to tamper with this option unless strictly necessary.

_**Value Type:**_ String

_**Default Value:**_ `ISV|abraunegg|OneDrive Client for Linux/vX.Y.Z-A-bcdefghi`

_**Config Example:**_ `user_agent = "ISV|CompanyName|AppName/Version"`

_**Additional Usage Notes:**_ The current value conforms the the Microsoft Graph API documentation for presenting an appropriate 'User-Agent' header and aligns to the registered 'application_id' that this application uses.

### webhook_enabled
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 

### webhook_expiration_interval
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 

### webhook_listening_host
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 

### webhook_listening_port
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 

### webhook_public_url
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 

### webhook_renewal_interval
_**Description:**_ 

_**Value Type:**_ 

_**Default Value:**_ 

_**Config Example:**_ 



## Command Line Interface (CLI) Only Options

### CLI Option: --auth-files
_**Description:**_

_**Usage Example:**_

### CLI Option: --auth-response
_**Description:**_

_**Usage Example:**_

### CLI Option: --confdir
_**Description:**_ This CLI option allows the user to specify where all the application configuration and relevant components are stored.

_**Usage Example:**_ `onedrive --confdir '~/.config/onedrive-business/'`

_**Additional Usage Notes:**_ If using this option, it must be specified each and every time the application is used. If this is ommited, the application default configuration directory will be used.

### CLI Option: --create-directory
_**Description:**_

_**Usage Example:**_

### CLI Option: --create-share-link
_**Description:**_

_**Usage Example:**_

### CLI Option: --destination-directory
_**Description:**_

_**Usage Example:**_

### CLI Option: --display-config
_**Description:**_ This CLI option will display the effective application configuration

_**Usage Example:**_ `onedrive --display-config`

### CLI Option: --display-sync-status
_**Description:**_

_**Usage Example:**_

### CLI Option: --force
_**Description:**_ This CLI option enables the force the deletion of data when a 'big delete' is detected

_**Usage Example:**_

### CLI Option: --force-sync
_**Description:**_

_**Usage Example:**_

### CLI Option: --get-file-link
_**Description:**_

_**Usage Example:**_

### CLI Option: --get-sharepoint-drive-id
_**Description:**_ This CLI option queries the OneDrive API and return's the Office 365 Drive ID for a given Office 365 SharePoint Shared Library that can then be used with 'drive_id' to sync a specific SharePoint Library.

_**Usage Example:**_ `onedrive --get-sharepoint-drive-id '*'` or `onedrive --get-sharepoint-drive-id 'PointPublishing Hub Site'`

### CLI Option: --logout
_**Description:**_ This CLI option removes this clients authentictaion status with Microsoft OneDrive. Any further application use will requrie the application to be re-authenticated with Microsoft OneDrive.

_**Usage Example:**_ `onedrive --logout`

### CLI Option: --modified-by
_**Description:**_

_**Usage Example:**_

### CLI Option: --monitor | -m
_**Description:**_ This CLI option controls the 'Monitor Mode' operational aspect of the client. When this option is used, the client will perform on-going syncs of data between Microsoft OneDrive and your local system. Local changes will be uploaded in near-realtime, whilst online changes will be downloaded on the next sync process. The frequency of these checks is governed by the 'monitor_interval' value.

_**Usage Example:**_ `onedrive --monitor` or `onedrive -m`

### CLI Option: --print-access-token
_**Description:**_ Print the current access token being used to access Microsoft OneDrive. 

_**Usage Example:**_ `onedrive --verbose --verbose --debug-https --print-access-token`

_**Additional Usage Notes:**_ Do not use this option if you do not know why you are wanting to use it. Be highly cautious of exposing this object. Change your password if you feel that you have inadvertantly exposed this token.

### CLI Option: --reauth
_**Description:**_ This CLI option controls the ability to re-authenticate your client with Microsoft OneDrive.

_**Usage Example:**_ `onedrive --reauth`

### CLI Option: --remove-directory
_**Description:**_

_**Usage Example:**_

### CLI Option: --single-directory
_**Description:**_

_**Usage Example:**_

### CLI Option: --source-directory
_**Description:**_

_**Usage Example:**_

### CLI Option: --sync | -s
_**Description:**_ This CLI option controls the 'Standalone Mode' operational aspect of the client. When this option is used, the client will perform a one-time sync of data between Microsoft OneDrive and your local system.

_**Usage Example:**_ `onedrive --sync` or `onedrive -s`

### CLI Option: --verbose | -v+
_**Description:**_

_**Usage Example:**_

### CLI Option: --with-editing-perms
_**Description:**_

_**Usage Example:**_

## Depreciated Configuration File and CLI Options
The following configuration options are no longer supported

### min_notify_changes
_**Description:**_ Minimum number of pending incoming changes necessary to trigger a GUI desktop notification.

_**Depreciated Config Example:**_ `min_notify_changes = "50"`

_**Depreciated CLI Option:**_ `--min-notify-changes '50'`

_**Reason for depreciation:**_ Application has been totally re-written. When this item was introduced, it was done so to reduce spamming of all events to the GUI desktop.

### CLI Option: --synchronize
_**Description:**_ Perform a synchronisation with Microsoft OneDrive

_**Depreciated CLI Option:**_ `--synchronize`

_**Reason for depreciation:**_ `--synchronize` has been depreciated in favour of `--sync` or `-s`