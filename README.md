# Dessert Release 🍰

Dessert Release is an Android app, built with Kotlin and Jetpack Compose, that displays a list of Android dessert release names (Cupcake, Donut, Eclair, ... Tiramisu) and lets you toggle between a linear (list) layout and a grid layout — with the chosen layout preference persisted across app launches using Jetpack **DataStore**.

## Features

- **Browse Android dessert releases** — a scrollable list of every historical Android dessert-name release, from Cupcake to Tiramisu.
- **Switch between layouts** — toggle between a linear list view (`LazyColumn`) and a grid view (`LazyVerticalGrid`) with a single tap.
- **Persisted layout preference** — the selected layout is saved with Jetpack DataStore (Preferences), so it's remembered the next time the app is opened.
- **Reactive UI state** — layout preference is exposed as a `StateFlow` and collected by the Compose UI, so the screen updates instantly when the preference changes.

## Tech stack

- **Kotlin**
- **Jetpack Compose** (Material 3, `LazyColumn`, `LazyVerticalGrid`) for the UI
- **Jetpack DataStore** (`androidx.datastore:datastore-preferences`) for persisting the layout preference
- **ViewModel** (`androidx.lifecycle:lifecycle-viewmodel-compose`) for UI state management
- **Navigation Compose** (`androidx.navigation:navigation-compose`)
- **Kotlin Coroutines / Flow** for observing preference changes

## Project structure

```
app/src/main/java/com/example/dessertrelease/
├── MainActivity.kt                     # App entry point
├── DesertReleaseApplication.kt         # Application class; provides UserPreferencesRepository
├── data/
│   ├── UserPreferenceRepository.kt     # Reads/writes the layout preference via DataStore
│   └── local/
│       └── LocalDessertReleaseData.kt  # Static list of dessert release names
└── ui/
    ├── DessertReleaseScreen.kt         # Composables for the linear and grid layouts + toggle button
    ├── DessertReleaseViewModel.kt      # Exposes UI state (isLinearLayout) and handles layout selection
    └── theme/                          # Compose theme (color, typography)
```

## Getting started

### Prerequisites

- [Android Studio](https://developer.android.com/studio) (latest stable release)
- JDK 11+
- An Android device or emulator running **API 24 (Android 7.0)** or higher

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/SamratVsn/Dessert-Release.git
   ```
2. Open the project in Android Studio.
3. Let Gradle sync and download dependencies.
4. Run the app on an emulator or physical device.

Alternatively, build from the command line:

```bash
./gradlew assembleDebug
```

## How it works

1. `LocalDessertReleaseData` provides the static list of dessert release names shown on screen.
2. `DessertReleaseViewModel` exposes a `StateFlow<DessertReleaseUiState>` built from `UserPreferencesRepository.isLinearLayout`, which reads the current layout choice out of DataStore.
3. `DessertReleaseScreen` renders the list as either `DessertReleaseLinearLayout` (a `LazyColumn`) or `DessertReleaseGridLayout` (a `LazyVerticalGrid`), depending on `isLinearLayout`.
4. Tapping the toggle icon in the top bar calls `selectLayout()`, which flips the flag and persists it via `userPreferencesRepository.saveLayoutPreference()` — so the choice survives app restarts.

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open a pull request or file an issue.

## License

No license has been specified for this project yet. If you plan to reuse this code, please check with the repository owner.
