# **AudiobookDiscovery Runtime Configuration Reference**

\
This document defines all runtime configuration keys used by the **AudiobookDiscovery** application.  

Values are stored and retrieved through \`RegistryHelper\` in:

```
AudiobookDiscovery.Core ➜ Services ➜ RegistryHelper.cs
```

All keys live under the following registry structure:

```
HKEY\_CURRENT\_USER
└── Software
    └── AudiobookDiscovery
        ├── SQL
        └── Runtime
```

<br />

## **## 1. SQL Configuration**

\
**### SQL → Page**

Controls which SQL page is used when retrieving preposed search rows.

| Key  | Type | Default | Description                                                 |
| :--- | :--- | :------ | :---------------------------------------------------------- |
| Page | int  | 0       | The SQL page number used by \`GetPreposedSearchRowsAsync\`. |

\
**Example:**

```
SQL
└── Page = 0
```

<br />

## ## 2. Runtime Configuration

\
**### Runtime → QueueDelayMilliseconds**

Controls the delay between each queued job processed by \`WorkerQueueController\`.

| Key                    | Type | Default | Description                                  |
| :--------------------- | :--- | :------ | :------------------------------------------- |
| QueueDelayMilliseconds | int  | 500     | Milliseconds to wait between each queue job. |

<br />

Used inside:

```
WorkerQueueController.StartAsync
```

<br />

**Example:**

```
Runtime
└── QueueDelayMilliseconds = 500
```

<br />

**### Runtime → CancelDelaySeconds**

Controls how long the UI waits before resetting state after a cancellation.

| Key                | Type | Default | Description                                                                 |
| :----------------- | :--- | :------ | :-------------------------------------------------------------------------- |
| CancelDelaySeconds | int  | 60      | Seconds to wait before resetting the Discovery pipeline after cancellation. |

\
Used inside:

```
DiscoveryViewModel.CancelDiscovery
```

Example:

```
Runtime
└── CancelDelaySeconds = 60
```

<br />

**### Runtime → LogFile**

Defines the log file path template used by \`StatusService\`.

| Key     | Type   | Default                                 | Description                                                             |
| :------ | :----- | :-------------------------------------- | :---------------------------------------------------------------------- |
| LogFile | string | C:\AudiobookWFP\Logs\Audiobook\_{0}.log | Path template for log files. \`{0}\` is replaced with the current date. |

\
Used inside:

```
StatusService.GetLogFilePath()
```

Example:

```
Runtime
└── LogFile = C:\AudiobookWFP\Logs\Audiobook\_{0}.log
```

The \`{0}\` placeholder is replaced with:

```
yyyy-MM-dd
```

Example resolved path:

```
C:\AudiobookWFP\Logs\Audiobook_2026-09-23.log
```

<br />

## ## 3. Summary Table



| Section | Key                    | Type   | Default                                 | Description           |
| :------ | :--------------------- | :----- | :-------------------------------------- | :-------------------- |
| SQL     | Page                   | int    | 0                                       | SqlAsyncService       |
| Runtime | QueueDelayMilliseconds | int    | 500                                     | WorkerQueueController |
| Runtime | CancelDelaySeconds     | int    | 60                                      | DiscoveryViewModel    |
| Runtime | LogFile                | string | C:\AudiobookWFP\Logs\Audiobook\_{0}.log | StatusService         |

<br />

## ## 4. Notes

* All keys are optional; defaults are applied automatically.
* Missing directories for \`LogFile\` are created at runtime.
* \`QueueDelayMilliseconds\` and \`CancelDelaySeconds\` are independent.
* UI may override values at runtime if desired.

<br />
