# KVision Codebase Map & Comprehensive API Reference

This document contains a complete technical index of all C++ classes, QML components, properties, methods, signals, and architectural relationships.

---

## 1. Registered QML Module Types & Singletons

| QML Type Name | Registered Module | C++ Type | Kind | Header / Impl |
| :--- | :--- | :--- | :--- | :--- |
| `Context` | `CCTV_Viewer.Core 1.0` | [`Context`](file:///home/robert/cctv/kvision/src/context.h) | Singleton | [`src/context.h`](file:///home/robert/cctv/kvision/src/context.h) / [`src/context.cpp`](file:///home/robert/cctv/kvision/src/context.cpp) |
| `SystemStats` | `CCTV_Viewer.Core 1.0` | [`SystemStats`](file:///home/robert/cctv/kvision/src/systemstats.h) | Singleton | [`src/systemstats.h`](file:///home/robert/cctv/kvision/src/systemstats.h) / [`src/systemstats.cpp`](file:///home/robert/cctv/kvision/src/systemstats.cpp) |
| `Clipboard` | `CCTV_Viewer.Utils 1.0` | [`Clipboard`](file:///home/robert/cctv/kvision/src/clipboard.h) | Singleton | [`src/clipboard.h`](file:///home/robert/cctv/kvision/src/clipboard.h) |
| `EventFilter` | `CCTV_Viewer.Utils 1.0` | [`EventFilter`](file:///home/robert/cctv/kvision/src/eventfilter.h) | Instantiable | [`src/eventfilter.h`](file:///home/robert/cctv/kvision/src/eventfilter.h) / [`src/eventfilter.cpp`](file:///home/robert/cctv/kvision/src/eventfilter.cpp) |
| `HikvisionManager` | `CCTV_Viewer.Hikvision 1.0` | [`HikvisionManager`](file:///home/robert/cctv/kvision/src/hikvisionmanager.h) | Singleton | [`src/hikvisionmanager.h`](file:///home/robert/cctv/kvision/src/hikvisionmanager.h) / [`src/hikvisionmanager.cpp`](file:///home/robert/cctv/kvision/src/hikvisionmanager.cpp) |
| `HikvisionISAPI` | `CCTV_Viewer.Hikvision 1.0` | [`HikvisionISAPI`](file:///home/robert/cctv/kvision/src/hikvisionisapi.h) | Singleton | [`src/hikvisionisapi.h`](file:///home/robert/cctv/kvision/src/hikvisionisapi.h) / [`src/hikvisionisapi.cpp`](file:///home/robert/cctv/kvision/src/hikvisionisapi.cpp) |
| `HikvisionPlayer` | `CCTV_Viewer.Hikvision 1.0` | [`HikvisionPlayer`](file:///home/robert/cctv/kvision/src/hikvisionplayer.h) | QuickPaintedItem | [`src/hikvisionplayer.h`](file:///home/robert/cctv/kvision/src/hikvisionplayer.h) / [`src/hikvisionplayer.cpp`](file:///home/robert/cctv/kvision/src/hikvisionplayer.cpp) |
| `HikvisionArchivePlayer` | `CCTV_Viewer.Hikvision 1.0` | [`HikvisionArchivePlayer`](file:///home/robert/cctv/kvision/src/hikvisionarchiveplayer.h) | QuickPaintedItem | [`src/hikvisionarchiveplayer.h`](file:///home/robert/cctv/kvision/src/hikvisionarchiveplayer.h) / [`src/hikvisionarchiveplayer.cpp`](file:///home/robert/cctv/kvision/src/hikvisionarchiveplayer.cpp) |
| `HikvisionDownloader` | `CCTV_Viewer.Hikvision 1.0` | [`HikvisionDownloader`](file:///home/robert/cctv/kvision/src/hikvisiondownloader.h) | Instantiable | [`src/hikvisiondownloader.h`](file:///home/robert/cctv/kvision/src/hikvisiondownloader.h) / [`src/hikvisiondownloader.cpp`](file:///home/robert/cctv/kvision/src/hikvisiondownloader.cpp) |
| `QmlAVPlayer` | `CCTV_Viewer.Multimedia 1.0`| [`QmlAVPlayer`](file:///home/robert/cctv/kvision/src/qmlav/src/qmlavplayer.h) | Instantiable | [`src/qmlav/src/qmlavplayer.h`](file:///home/robert/cctv/kvision/src/qmlav/src/qmlavplayer.h) / [`src/qmlav/src/qmlavplayer.cpp`](file:///home/robert/cctv/kvision/src/qmlav/src/qmlavplayer.cpp) |
| `ViewportsLayoutItem` | `CCTV_Viewer.Models 1.0` | [`ViewportsLayoutItem`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.h#L13) | Instantiable | [`src/viewportslayoutmodel.h`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.h) / [`src/viewportslayoutmodel.cpp`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.cpp) |
| `ViewportsLayoutModel` | `CCTV_Viewer.Models 1.0` | [`ViewportsLayoutModel`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.h#L43) | ListModel | [`src/viewportslayoutmodel.h`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.h) / [`src/viewportslayoutmodel.cpp`](file:///home/robert/cctv/kvision/src/viewportslayoutmodel.cpp) |
| `ViewportsLayoutsCollectionModel` | `CCTV_Viewer.Models 1.0` | [`ViewportsLayoutsCollectionModel`](file:///home/robert/cctv/kvision/src/viewportslayoutscollectionmodel.h) | ListModel | [`src/viewportslayoutscollectionmodel.h`](file:///home/robert/cctv/kvision/src/viewportslayoutscollectionmodel.h) / [`src/viewportslayoutscollectionmodel.cpp`](file:///home/robert/cctv/kvision/src/viewportslayoutscollectionmodel.cpp) |
| `NvrStatusManager` | Context Property | [`NvrStatusManager`](file:///home/robert/cctv/kvision/src/nvrstatusmanager.h) | Singleton | [`src/nvrstatusmanager.h`](file:///home/robert/cctv/kvision/src/nvrstatusmanager.h) / [`src/nvrstatusmanager.cpp`](file:///home/robert/cctv/kvision/src/nvrstatusmanager.cpp) |
| `image://cctv/...` | Image Provider | [`ThumbnailProvider`](file:///home/robert/cctv/kvision/src/thumbnailprovider.h) | ImageProvider | [`src/thumbnailprovider.h`](file:///home/robert/cctv/kvision/src/thumbnailprovider.h) / [`src/thumbnailprovider.cpp`](file:///home/robert/cctv/kvision/src/thumbnailprovider.cpp) |

---

## 2. Exhaustive C++ Class API Reference

### [`Context`](file:///home/robert/cctv/kvision/src/context.h) (`CCTV_Viewer.Core`)
* **Thread affinity**: Main GUI Thread.
* **Responsibilities**: Application orchestration, configuration bridging, runtime localization, memory trimming, and inter-process auxiliary spawning.
* **Q_PROPERTY**:
  * `config` (`Config*`) – Global config object instance.
  * `isAuxiliary` (`bool`) – True if launched with `--auxiliary`.
  * `auxiliaryId` (`int`) – Numeric ID of current auxiliary process.
  * `isFirstRun` (`bool`) – True if `--first-run` flag was passed.
  * `mockNewVersion` (`bool`) – For UI update testing.
* **Invokables (`Q_INVOKABLE`)**:
  * `void setLanguage(const QString &langCode)` – Dynamically removes old `QTranslator` and installs new locale `.qm` file. Emits `languageChanged()`.
  * `QString getLanguage() const` – Returns active language code.
  * `void startAuxiliaryProcess()` – Spawns child process `./klens --auxiliary <nextId>`.
  * `void trimMemory()` – Executes `malloc_trim(0)` on Linux glibc.
  * `bool mkpath(const QString &path)` / `bool dirExists(const QString &path)` / `QString homePath()` / `QUrl pathToUrl(const QString &path)` – Filesystem path utilities.
  * `QVariant readSetting(const QString &category, const QString &key, const QVariant &defaultVal)` – Reads from `QSettings`.
  * `void writeSetting(const QString &category, const QString &key, const QVariant &value)` – Writes to `QSettings` and calls `sync()`.
  * `QString readLocalFile(const QString &filePath)` – Loads markdown / text files for modal dialogs.
* **Signals**: `languageChanged()`, `configFileChanged()`.

---

### [`HikvisionManager`](file:///home/robert/cctv/kvision/src/hikvisionmanager.h) (`CCTV_Viewer.Hikvision`)
* **Thread affinity**: Main GUI Thread + Background `ptzWorkerLoop` thread.
* **Responsibilities**: Session pooling (`NET_DVR_Login_V40`), PTZ zoom command queue, async device discovery, and channel I-Frame force injection.
* **Login serialization & throttling**: All `NET_DVR_Login_V40` attempts for one device run serialized behind a per-device mutex (`loginMutexFor()`), and failed logins start a per-device cooldown (`recordLoginFailure()`: 15 s–2 min backoff for transient errors, 5 min for wrong credentials, 30 min for SDK error 153 `NET_DVR_USER_LOCKED` — the device's "Illegal Login Lock"). While a cooldown is active, `loginToDevice()` fast-fails without device I/O. This prevents the burst of simultaneous same-account logins (live players + thumbnails + status poller + ISAPI fallback) that trips the device lock and breaks every camera channel with "SDK login failed (153)".
* **Invokables & Methods**:
  * `QVariantList discoverCameras(QString ip, int port, int httpPort, QString user, QString pass)` (synchronous).
  * `void discoverCamerasAsync(QString ip, int port, int httpPort, QString user, QString pass)` – Executes discovery on a separate `QThread`, emitting `discoveryFinished()`.
  * `LONG loginShared(QString ip, int port, QString user, QString pass, NET_DVR_DEVICEINFO_V40 *info)` – Reuses existing `lUserID` for given host/credentials; serialized per device (double-checked) so concurrent callers share one login.
  * `void logoutShared(QString ip)` – Decrements ref-count and calls `NET_DVR_Logout` when 0.
  * `void releaseShared(QString ip, LONG userID)` – Like `logoutShared()`, but only decrements if `userID` is still the active shared session (safe when the session was replaced/force-logged-out).
  * `int lastLoginError(QString ip)` / `qint64 loginCooldownRemainingMs(QString ip)` – Inspect the recorded login failure reason and remaining throttle window.
  * `void ptzZoom(QString ip, int port, QString user, QString pass, int channelId, int command, bool stop)` – Enqueues PTZ commands to `ptzWorkerLoop` thread to prevent GUI frame drops.
  * `void forceIFrame(QString ip, int port, QString user, QString pass, int channelId)` – Invokes `NET_DVR_MakeKeyFrameSub` for fast stream start.
* **Signals**: `sessionStatusChanged(QString ip, bool loggedIn)`, `discoveryFinished(QString ip, QVariantList cameras, bool success, QString errorMsg)`.

---

### [`HikvisionArchivePlayer`](file:///home/robert/cctv/kvision/src/hikvisionarchiveplayer.h) (`CCTV_Viewer.Hikvision`)
* **Inherits**: `QQuickPaintedItem`.
* **Responsibilities**: High-performance archive video/audio playback from Hikvision NVRs via `NET_DVR_PlayBackByTime_V40`; also used as the live SDK preview player when the "Use SDK instead of RTSP" (`useSdkMedia`) recorder option is enabled.
* **Live preview auto-recovery**: `startLive()` failures (SDK login error or dead session) schedule an epoch-guarded single-shot retry (`scheduleLiveRetry()`); retries that fall inside the manager's login cooldown fast-fail without device I/O, so the preview resumes automatically once the device allows logins again. After ~5 real device attempts the loop gives up and leaves the status message visible. Login failures surface a human-readable reason (`hikSdkLoginErrorText()`), e.g. error 153 = account locked by the device's "Illegal Login Lock".
* **Q_PROPERTY**:
  * `recorderIp` (`QString`), `channelId` (`int`), `port` (`int`), `username` (`QString`), `password` (`QString`).
  * `currentPlayheadMs` (`qint64`) – Current playback position in Unix milliseconds.
  * `isPlaying` (`bool`), `isPaused` (`bool`), `fps` (`int`).
  * `videoWidth` (`int`), `videoHeight` (`int`).
  * `volume` (`qreal` 0.0..1.0), `muted` (`bool`).
  * `playerStatusMessage` (`QString`).
* **Invokables**:
  * `void playAtTime(const QDateTime &dateTime)` – Starts playback at target timestamp.
  * `void setPlaybackSpeed(int speed)` – Supported: `1, 2, 4, 8` (fast-forward) or `-1, -2, -4, -8` (reverse).
  * `void pause()` / `void resume()` / `void stop()`.
  * `bool saveCurrentFrame(const QString &filePath)` – Dumps current RGB32 buffer to file.
* **Callbacks & Pipelines**:
  * `PlayDataCallBack` $\to$ feeds raw packets to SDK player core.
  * `DecCallBack` $\to$ receives decoded YV12 frames, schedules `YV12ToRGBTask` in `FrameBufferPool`.
  * `AudioCallBack` $\to$ receives 16-bit PCM audio, dynamically adapts `QAudioFormat` and writes to `QAudioOutput`.

---

### [`HikvisionISAPI`](file:///home/robert/cctv/kvision/src/hikvisionisapi.h) (`CCTV_Viewer.Hikvision`)
* **Thread affinity**: Main GUI Thread (`QNetworkAccessManager`).
* **Responsibilities**: HTTP REST queries for archive metadata, recording spans, and monthly calendar availability.
* **Invokables**:
  * `void searchRecordings(const QVariantMap &recorderInfo, int channelId, const QDateTime &start, const QDateTime &end)` – Queries `/ISAPI/ContentMgmt/search` with Digest Authentication.
  * `void searchMonthAvailability(const QVariantMap &recorderInfo, int channelId, int year, int month)` – Returns days containing recordings.
  * `void cancelAllSearches()` – Aborts all pending HTTP network requests.
* **Signals**:
  * `searchFinished(QString sessionId, int channelId, QVariantList segments)`.
  * `searchFailed(QString sessionId, int channelId, QString errorMessage)`.
  * `monthAvailabilityFinished(QString sessionId, int channelId, int year, int month, QList<int> availableDays)`.

---

### [`HikvisionDownloader`](file:///home/robert/cctv/kvision/src/hikvisiondownloader.h) (`CCTV_Viewer.Hikvision`)
* **Thread affinity**: Main GUI Thread + Background `QProcess` (FFmpeg).
* **Responsibilities**: Segmented archive clip downloading via `NET_DVR_GetFileByTime_V40` and remuxing to `.mp4`.
* **Q_PROPERTY**:
  * `isDownloading` (`bool`), `isConverting` (`bool`).
  * `progress` (`int` 0..100) – Current segment progress.
  * `overallProgress` (`int` 0..100) – Total batch progress.
  * `statusText` (`QString`).
* **Invokables**:
  * `void startDownload(const QVariantMap &recorderInfo, int channelId, const QDateTime &start, const QDateTime &end, const QString &saveFilePath)`.
  * `void stopDownload()`.
* **Signals**: `downloadFinished(bool success, const QString &message)`.

---

### [`NvrStatusManager`](file:///home/robert/cctv/kvision/src/nvrstatusmanager.h) (Context Property)
* **Thread affinity**: Main GUI Thread + Background `NvrStatusWorker` on `QThread`.
* **Responsibilities**: Background health polling (every 60s) for offline channels, high CPU, S.M.A.R.T. disk errors, and unformatted drives.
* **Q_PROPERTY**:
  * `hasErrors` (`bool`), `errors` (`QVariantList`), `checkedRecorders` (`QVariantList`).
  * `isChecking` (`bool`), `monitoringEnabled` (`bool`).
  * `checkOffline` (`bool`), `checkCpu` (`bool`), `checkHw` (`bool`), `checkHdd` (`bool`), `checkUnformatted` (`bool`), `checkFull` (`bool`).
* **Invokables**:
  * `void checkNow()` – Forces immediate worker run.
  * `void onRecordersChanged()` – Reloads NVR list from `Hikvision/recordersJson`.
  * `bool isRecorderMuted(const QString &name)` / `void setRecorderMuted(const QString &name, bool muted)`.
* **Signals**: `hasErrorsChanged()`, `errorsChanged()`, `checkedRecordersChanged()`.

---

### [`QmlAVPlayer`](file:///home/robert/cctv/kvision/src/qmlav/src/qmlavplayer.h) (`CCTV_Viewer.Multimedia`)
* **Thread affinity**: Main GUI Thread + `QmlAVThread` (Demuxer loop) + `QmlAVDecoder` worker tasks.
* **Responsibilities**: Zero-latency RTSP streaming and local media playback via FFmpeg.
* **Q_PROPERTY**:
  * `source` (`QUrl`) – RTSP or file stream URL.
  * `videoSurface` (`QAbstractVideoSurface*`) – Bound to QML `VideoOutput`.
  * `playbackState` (`QMediaPlayer::State`), `status` (`QMediaPlayer::MediaStatus`).
  * `fps` (`int`), `volume` (`double`), `muted` (`bool`).
  * `hasVideo` (`bool`), `hasAudio` (`bool`).
  * `avOptions` (`QVariantMap`) – Demuxer/decoder dictionary (e.g. `rtsp_transport`, `stimeout`).
* **Invokables & Slots**:
  * `void play()`, `void stop()`, `double bytesRead() const`.

---

## 3. QML Component Tree & Interactions

```
RootWindow.qml (Primary UI Window) / AuxiliaryWindow.qml (Multi-Monitor Auxiliary Window)
├── ToolBar (Dynamic multi-row Flow top dock with QtQuick.Shapes background, Layout/Views selector, Mute, Fullscreen, Playback trigger, Add NVR, EventFilter auto-hide)
├── SideBar.qml (Collapsible left panel using StyledScrollBar.qml across settings tabs)
│   ├── NVR TreeView / ListView (NVR entries & channel items)
│   ├── Channel status badges (Online/Offline indicator)
│   └── Drag-and-drop triggers for dragging camera to grid tiles
├── StyledScrollBar.qml (Shared high-contrast vertical/horizontal ScrollBar component)
├── ViewportsLayout.qml (Central Matrix Container)
│   ├── Grid / Flow layout (1x1, 2x2, 3x3, 4x4, custom spans)
│   ├── Tile DropAreas (Handles camera drop, swap, clear)
│   └── Instantiates N x Player.qml
│       ├── qmlAvPlayer1 & qmlAvPlayer2 (Dual player for smooth stream switching)
│       ├── HikvisionPlayer (Optional live SDK stream)
│       ├── QuickPlayback loader (In-tile instant rewind)
│       ├── OSD Overlay (Camera title, Bitrate, FPS, Connection state)
│       ├── Digital Zoom & 1:1 pixel crop container
│       └── Right-click ContextMenu (Stream selection, Aspect ratio, Snapshot, Remove)
├── PlaybackWindow.qml (Separate archive playback window)
│   ├── Channel selector sidebar
│   ├── HikvisionISAPI search trigger
│   ├── 24-hour interactive Timeline Bar (Recording segments, scrubbing, time ruler)
│   ├── Calendar DatePicker (Highlights days with recordings)
│   ├── HikvisionArchivePlayer (SDK player instance with DecCallBack)
│   └── Playback controls (Play, Pause, Speed -8x..+8x, Step frame, Volume)
├── DownloadDialog.qml (Modal for batch video export)
│   ├── Time range pickers
│   └── HikvisionDownloader integration (Progress bar, FFmpeg remuxing)
├── NvrCamerasWindow.qml & NvrSettingsPanel.qml (NVR & Camera configuration modals)
└── NvrStatusDialog.qml (Diagnostic report modal for NVR errors)
```
