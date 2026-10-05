<div align="center">

# 🎧 SuperPodcast
### Modern Native Android Podcast Streaming, Discovery & RSS Management Suite

[![Android](https://img.shields.io/badge/Android-SDK%2024%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://developer.android.com/)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0%2B-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Media3 ExoPlayer](https://img.shields.io/badge/Media-ExoPlayer%20Media3-E10098?style=for-the-badge)](https://developer.android.com/media/media3)
[![Room](https://img.shields.io/badge/Storage-Room%20SQLite-4285F4?style=for-the-badge&logo=sqlite&logoColor=white)](https://developer.android.com/training/data-storage/room)
[![WorkManager](https://img.shields.io/badge/Background-WorkManager-00C853?style=for-the-badge)](https://developer.android.com/topic/libraries/architecture/workmanager)
[![License](https://img.shields.io/badge/License-MIT-CEFF00?style=for-the-badge&logoColor=black)](LICENSE)

<br/>

**An end-to-end native Android audio/video streaming and podcast management application built with Kotlin, Apple iTunes Search API, Room SQLite database, Media3 ExoPlayer, and WorkManager background synchronization.**

<br/>

[Features](#-key-features) •
[Architecture](#-architecture--tech-stack) •
[Background Sync](#-background-synchronization--notifications) •
[Installation](#-how-to-build-and-run) •
[License](#-license)

</div>

<br/>

---

## 📌 Technical Overview

**SuperPodcast** is a full-featured Android podcast client designed around modern reactive architecture. It integrates semantic mood-based podcast discovery via the Apple iTunes Search API, streaming for audio, video, and HLS protocols via Media3 ExoPlayer, custom namespaced XML pull parsing for RSS feeds, local SQLite persistence via Room with reactive Kotlin `Flow`, and automated background episode polling with WorkManager.

---

## 🌟 Key Features

### 🔍 1. Search & Semantic Discovery
- **iTunes Search Integration**: Asynchronous podcast catalog search powered by Retrofit and Kotlin Coroutines.
- **Vibe & Mood Scoring Engine**: Analyzes show titles, artist info, and descriptions against curated keywords to score and rank podcasts by vibe compatibility (0–100%).
- **Curated Mood Chips**: Instant semantic filters (☕ *Rainy Loft*, 🔥 *High Octane*, 🕵️ *True Noir 2AM*, 🧠 *Mind Lab*, 🍿 *Pop & Banter*).
- **Surprise Vibe Generator**: Randomized mood generator with vinyl record rotation animations.

### 📜 2. RSS & Episode Management
- **Namespaced XML Pull Parser**: Custom XML parser processing standard RSS tags (`<title>`, `<guid>`, `<pubDate>`, `<enclosure>`) alongside iTunes namespaced extensions (`<content:encoded>`, `<media:content>`).
- **Media Type Detection**: Automatic MIME type inspection distinguishing audio streams from MP4/HLS video streams.
- **Rich Episode Catalog**: Formatted release dates, media type tags, playback duration, and parsed HTML show notes.

### 🎬 3. High-Performance Media Playback
- **Media3 ExoPlayer Engine**: Native hardware-accelerated playback for MP3, AAC, and MP4 media.
- **Adaptive HLS Streaming**: Full support for HTTP Live Streaming (`.m3u8` / `application/x-mpegURL`) feeds.
- **Lifecycle-Aware Playback**: Audio playback survives screen rotation and activity configuration transitions while safely releasing resources in `onDestroy()`.

### 💾 4. Subscriptions & Local Persistence
- **Room Database Architecture**: Local SQLite persistence caching subscribed shows with indexed iTunes track IDs.
- **Reactive UI Pipeline**: Real-time database observation and instant UI state propagation via Kotlin Coroutines `Flow`.
- **Alphabetical Library Index**: Clean subscriptions screen sorted alphabetically (A–Z) with instant detail view navigation.
- **One-Tap Subscriptions**: Reactive subscribe/unsubscribe toggle synchronized across the entire app.

---

## 🔄 Background Synchronization & Notifications

- **WorkManager Periodic Workers**: Scheduled background sync checks (15-minute polling interval) with network constraint validation.
- **GUID Episode Tracking**: Tracks latest episode GUIDs via `SharedPreferences` to detect new releases without false-positive alerts on initial subscription.
- **Notification Channels (API 26+)**: Configured notification channels with default priority and permission handling for Android 13+ (`POST_NOTIFICATIONS`).
- **Dual Notification Strategy**:
  - **Foreground Banner**: In-app `BroadcastReceiver` delivering non-intrusive Toast alerts while active.
  - **Background Push**: System notification drawer alerts with `BigTextStyle` expanders and direct `PendingIntent` navigation to new episodes.

---

## 🛠️ Architecture & Tech Stack

```
com.sheikhnaim.superpodcast
├── api/            # Retrofit iTunes Search API client & models
├── data/           # Room Database, DAOs (SubscriptionDao), and Entities
├── player/         # Media3 ExoPlayer controllers & playback services
├── parser/         # Custom XML Pull Parser for RSS 2.0 & iTunes feeds
├── ui/             # Activities, Adapters, ViewHolders, and Custom Views
└── worker/         # WorkManager background sync workers & notification helpers
```

- **Language**: Kotlin 2.0+
- **Architecture**: MVVM / Clean Architecture + Repository Pattern
- **Async Concurrency**: Kotlin Coroutines & `Flow`
- **Database**: Room (SQLite) with KSP
- **Networking**: Retrofit 2 + OkHttp 3
- **Media Engine**: AndroidX Media3 ExoPlayer
- **Background Tasks**: AndroidX WorkManager
- **Image Caching**: Glide 4
- **UI Components**: Material Design 3

---

## 🚀 How to Build and Run

### Prerequisites
- **Android Studio** Ladybug (2024.2+) or newer
- **Android SDK**: Minimum SDK 24 (Android 7.0), Target SDK 34+
- **JDK**: OpenJDK 17+

### Steps
1. **Clone the repository**:
   ```bash
   git clone https://github.com/snaimio/superpodcast.git
   ```
2. **Open in Android Studio**:
   - Open Android Studio $\rightarrow$ **File > Open** $\rightarrow$ select the cloned `superpodcast` directory.
3. **Sync Gradle**:
   - Allow Android Studio to download dependencies and sync Gradle.
4. **Run Application**:
   - Select an emulator or connected physical Android device and press **Run 'app'** (`Shift + F10`).

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
