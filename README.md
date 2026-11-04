# PhysicsMate

**A native Android toolkit for physics calculations and mathematical computation.**

![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/language-Java-orange?logo=openjdk&logoColor=white)
![Minimum SDK](https://img.shields.io/badge/minimum%20SDK-26-blue)
![Status](https://img.shields.io/badge/status-work%20in%20progress-yellow)

PhysicsMate is a personal Android development project that brings together physics calculators, symbolic and numerical mathematics tools, and a small collection of built-in formula notes.

> **Current codebase:** This repository is the refactored successor to the earlier [Physics-Mate](https://github.com/NoRancidIntentions/Physics-Mate) implementation. The newer version reorganizes the application around fragments, shared calculation utilities, and AndroidX navigation.

---

## Contents

- [Features](#features)
- [Implementation and Architecture](#implementation-and-architecture)
- [Technology Stack](#technology-stack)
- [Build and Run](#build-and-run)
- [Project Structure](#project-structure)
- [Current Development Status](#current-development-status)
- [Related Repository](#related-repository)
- [License](#license)

---

## Features

The list below distinguishes implemented calculators from screens that are currently placeholders.

### Physics

| Area | Implemented functionality |
|---|---|
| **Newtonian gravitation** | Calculate gravitational force, either mass, or the separation from the other quantities using Newton's law of universal gravitation. |
| **Escape velocity** | Calculate escape velocity, the attracting body's mass, or its radius. |
| **Special relativity** | Length-contraction calculator: determine proper length, contracted length, or relative speed when the other two values are supplied. |

The following topics are visible in the navigation but **do not yet have working calculator implementations**: time dilation, gravitational potential, gravitational potential energy, gravitational acceleration, orbital velocity, Kepler's law, Jeans mass, and Schwarzschild radius.

The implemented gravitation calculators use SI-unit inputs and outputs.

### Mathematics

| Tool | Functionality |
|---|---|
| **Variable Solver** | Numerically solve a system of equations in multiple variables. Equation input rows can be added or removed dynamically. |
| **Expression Evaluator** | Evaluate a mathematical function at user-supplied variable values. For example, evaluate `sin(x)*y` with assignments such as `x = pi, y = e`. |
| **Derivative Calculator** | Compute higher-order derivatives, display a simplified symbolic result, and plot the function and derivative over a selected range. |
| **Integral Calculator** | Compute higher-order and definite integrals, display simplified symbolic results, and plot the integrand and its integral over a selected range. |
| **Orthonormalisation** | Orthonormalise a set of input vectors using the symbolic mathematics backend. |
| **Vector Addition** | Add vectors represented in Cartesian components, polar coordinates, or direction-cosine form. |
| **Eigenvalue and Eigenvector Calculator** | Calculate eigenvalues and eigenvectors of square matrices. The interface accepts matrix dimensions from 1 to 11. |

### Formula Notes

The Notes screen displays built-in example formulas grouped under:

- **Gravity:** Newton's law of gravitation and gravitational potential energy.
- **Electricity & Magnetism:** Coulomb's law and Gauss's law.

The current screen is primarily a viewer for built-in examples. Although the underlying model has methods for adding topics and formulas, a complete user-facing editor and persistent storage across app launches have not been implemented.

### Interface

- **Custom mathematical keyboard** for entering expressions.
- **Mathematical expression rendering** with LaTeX-style formatting.
- **Copy-to-clipboard support** for calculator results.
- **Graph plotting** in the calculus tools.
- **Tabbed Home screen** separating Physics, Maths, and External Links.

---

## Implementation and Architecture

The current codebase separates the application into UI, model, and shared utility packages.

- **Java and AndroidX Fragments** are used for the calculator screens.
- **AndroidX Navigation** manages the main navigation destinations.
- **View Binding** is enabled for layouts.
- **Lifecycle ViewModels and LiveData** are used in the Notes and Settings areas.
- Shared expression parsing, numerical evaluation, symbolic operations, formatting, and graph helpers are centralised in `Custom_methods.java`.
- A custom keyboard is shared across calculator screens.

The project is an educational and exploratory application. The presence of a calculator interface should not be interpreted as validation of its numerical accuracy for research or safety-critical use.

---

## Technology Stack

### Project Configuration

| Component | Version / Setting |
|---|---|
| **Language** | Java |
| **Java source / target compatibility** | Java 11 |
| **Build scripts** | Gradle Kotlin DSL |
| **Android Gradle Plugin** | 8.12.0 |
| **Gradle distribution configured** | 8.13 |
| **Compile SDK** | 35 |
| **Target SDK** | 35 |
| **Minimum SDK** | 26 (Android 8.0) |
| **Application ID** | `com.example.physicsmate` |

### Main Dependencies

| Library | Purpose |
|---|---|
| [Symja / Matheclipse](https://github.com/axkr/symja_android_library) | Symbolic mathematics, expression evaluation, equation solving, differentiation, integration, and vector operations. |
| [MPAndroidChart](https://github.com/PhilJay/MPAndroidChart) | Plotting mathematical functions and results. |
| [AndroidMath](https://github.com/gregcockroft/AndroidMath) | Rendering mathematical notation. |
| [Material Components for Android](https://github.com/material-components/material-components-android) | Material UI components. |
| [AndroidX](https://developer.android.com/jetpack/androidx) | AppCompat, ConstraintLayout, Navigation, Lifecycle, and related Android libraries. |
| [Paris](https://github.com/airbnb/paris) | Programmatic view styling. |
| [Flexbox](https://github.com/google/flexbox-layout) | Flexible layouts. |

---

## Build and Run

### Requirements

- **Android Studio**
- **Android SDK Platform 35**
- **JDK 17 or newer** to run the Android Gradle Plugin build
- An Android device or emulator running **Android 8.0 (API 26) or newer**

The app's Java source and target compatibility are set to Java 11. This is separate from the JDK used to run Gradle.

### Open the Project

1. Clone the repository:

   ```bash
   git clone https://github.com/NoRancidIntentions/PhysicsMate2.git
   cd PhysicsMate2
   ```

2. Open the project root in Android Studio.
3. Install the required Android SDK components and synchronise the Gradle project.
4. Select a device or emulator and run the `app` configuration.

> **Android Studio note:** If project sync fails because the Gradle wrapper files are missing, add the standard wrapper files or configure Android Studio to use a local Gradle 8.13 installation.

### Build from the Command Line

The project is configured for Gradle 8.13. With a compatible local Gradle installation, build the debug APK using:

```bash
gradle :app:assembleDebug
```

Install it on a connected device using:

```bash
gradle :app:installDebug
```

> **Gradle wrapper note:** The repository currently contains `gradle/wrapper/gradle-wrapper.properties`, but does not contain `gradlew`, `gradlew.bat`, or `gradle-wrapper.jar`. Wrapper commands such as `./gradlew` will therefore not work from a fresh clone until the wrapper files are added.

The generated debug APK is normally written to:

```text
app/build/outputs/apk/debug/app-debug.apk
```

A release APK is currently included in the repository:

**[Download the release APK](app/release/app-release.apk)**

---

## Project Structure

The following is a high-level view of the source tree. Generated build output and IDE-specific files are intentionally omitted.

```text
PhysicsMate2/
+-- app/
|   +-- build.gradle.kts
|   +-- release/
|   |   `-- app-release.apk
|   `-- src/
|       `-- main/
|           +-- java/
|           |   `-- com/example/physicsmate/
|           |       +-- misc/
|           |       +-- model/
|           |       `-- ui/
|           `-- res/
+-- gradle/
|   `-- wrapper/
|       `-- gradle-wrapper.properties
+-- build.gradle.kts
+-- gradle.properties
+-- settings.gradle.kts
`-- README.md
```

### Main Source Packages

| Directory | Responsibility |
|---|---|
| `misc/` | Main activity, logging compatibility helper, and shared mathematical/computational utilities. |
| `model/` | Data models and adapters for Home topics and formula notes. |
| `ui/` | Custom keyboard, Physics and Maths screens, navigation, Notes, and Settings. |
| `res/` | Android layouts, navigation graph, themes, drawables, fonts, and other application resources. |

---

## Current Development Status

PhysicsMate is **a work in progress**. The main unfinished areas are:

- The **External Links** tab is currently a placeholder.
- The **Settings** screen is a scaffold; theme and font-size customisation are not implemented.
- Formula notes are currently built-in examples. A complete note editor and persistent storage are not implemented.
- Several physics topics appear in navigation but do not yet have calculator implementations; see the [Physics feature list](#physics).

---

## Related Repository

**Earlier implementation:** [NoRancidIntentions/Physics-Mate](https://github.com/NoRancidIntentions/Physics-Mate)

That repository contains the earlier activity-oriented version. **PhysicsMate2 is the newer refactored codebase** and is the recommended repository to use for the current project.

---

## License

This repository does not currently contain a license file. Until a license is added, the source code should be treated as **not licensed for reuse or redistribution**.
