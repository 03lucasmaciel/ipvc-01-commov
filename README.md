<a id="readme-top"></a>

<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Mobile Computing - Practical Exercise #1</h3>

  <p align="center">
    An Android application built with Jetpack Compose demonstrating fundamental concepts of declarative UI, state management, and user interaction.
    <br />
    <a href="https://github.com/03lucasmaciel/ipvc-01-commov"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/03lucasmaciel/ipvc-01-commov/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    ·
    <a href="https://github.com/03lucasmaciel/ipvc-01-commov/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#features">Features</a></li>
    <li><a href="#code-examples">Code Examples</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

This is **Practical Exercise #1** for the **Mobile Computing** course. The application demonstrates the fundamentals of building modern Android UIs using Jetpack Compose.

**PrimeiraApp** is a practical example showing how to build a modern user interface in Android using Compose. The application allows users to:

- Enter their name in a text field
- Click a button to receive a personalized greeting
- View a click counter
- Receive validation and visual feedback in real-time

The project covers essential Compose concepts including:

- Declarative UI development
- State management with `remember` and `mutableStateOf`
- Event handling with `onClick`
- Form validation and conditional UI rendering
- Material Design 3 components

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

- [![Kotlin][Kotlin-badge]][Kotlin-url]
- [![Android][Android-badge]][Android-url]
- [![Jetpack Compose][Compose-badge]][Compose-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->

## Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

- Android Studio (latest version recommended)
- Android SDK (API level 24 or higher)
- Kotlin 1.9.0 or higher

### Installation

1. Clone the repository
   ```sh
   git clone https://github.com/03lucasmaciel/ipvc-01-commov.git
   ```
2. Open the project in Android Studio
3. Wait for Gradle to sync and download dependencies
4. Run the application on an emulator or physical device

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- FEATURES -->

## Features

### Part A-B: Initial Structure

- Creation of `MainActivity`
- Composable `PrimeiraApp()` with `Column` and basic layout
- Usage of `MaterialTheme` for styling

### Part C: Text Field and State

- Input field using `OutlinedTextField`
- State management with `remember` and `mutableStateOf`
- Dynamic state updates with `onValueChange`

**Concept:** The `nome` state is reactive - any change in the field automatically updates the UI.

### Part D: Button and Result

- Addition of a `Button` with `onClick` event
- New `resultado` state to store the greeting
- Dynamic result display

### Part E: Click Counter

- New `cliques` state to count interactions
- Counter increment on button `onClick`
- Counter display in the UI

### Mini-Challenge: Validation and Visual Feedback

1. **Disable Button if Name is Empty** - Button is disabled when input is blank
2. **Show Error Message** - Red error text appears when validation fails
3. **Change Text Color When Valid** - Green text for valid input

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CODE EXAMPLES -->

## Code Examples

### State Management

```kotlin
var nome by remember { mutableStateOf("") }
OutlinedTextField(
    value = nome,
    onValueChange = { nome = it },
    label = { Text("Enter your name") }
)
```

### Button with Click Handler

```kotlin
var resultado by remember { mutableStateOf("") }
var cliques by remember { mutableStateOf(0) }

Button(onClick = {
    cliques++
    resultado = "Hello, $nome!"
}) {
    Text("Say Hello")
}
```

### Validation

```kotlin
val nomeValido = nome.isNotBlank()
Button(
    onClick = { ... },
    enabled = nomeValido
)

if (!nomeValido) {
    Text(
        text = "Name cannot be empty!",
        color = Color.Red
    )
}
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- COMPLETE CODE -->

## Complete Code

```kotlin
package com.example.myapplication

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.OutlinedTextField
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                Surface(modifier = Modifier.fillMaxSize()) {
                    PrimeiraApp()
                }
            }
        }
    }
}

@Composable
fun PrimeiraApp() {
    var nome by remember { mutableStateOf("") }
    var resultado by remember { mutableStateOf("") }
    var cliques by remember { mutableStateOf(0) }
    val nomeValido = nome.isNotBlank()

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "My first Compose app",
            style = MaterialTheme.typography.titleLarge
        )
        Spacer(modifier = Modifier.height(24.dp))

        OutlinedTextField(
            value = nome,
            onValueChange = { nome = it },
            label = { Text("Enter your name") }
        )

        if (!nomeValido) {
            Spacer(modifier = Modifier.height(8.dp))
            Text(
                text = "Name cannot be empty!",
                color = Color.Red
            )
        }

        Spacer(modifier = Modifier.height(16.dp))

        Button(
            onClick = {
                cliques++
                resultado = "Hello, $nome!"
            },
            enabled = nomeValido
        ) {
            Text("Say Hello")
        }

        Spacer(modifier = Modifier.height(24.dp))

        Text(
            text = resultado,
            color = if (nomeValido && resultado.isNotBlank()) Color.Green else Color.Black
        )
        Spacer(modifier = Modifier.height(8.dp))
        Text(text = "Clicks: $cliques")
    }
}
```

---

## Key Concepts

### 1. **Composables**

Functions annotated with `@Composable` that describe the UI declaratively.

### 2. **State with `remember` and `mutableStateOf`**

- `remember { }`: Retains value across recompositions
- `mutableStateOf("")`: Creates mutable state that triggers recomposition when changed

### 3. **Reactivity**

The UI is automatically updated when state changes, without the need to call manual update methods.

### 4. **Property Delegation**

```kotlin
var nome by remember { mutableStateOf("") }
```

Elegant Kotlin syntax that allows reading/writing to state like a normal property.

---

## Interaction Flow

```
User types name
    ↓
onChange triggers → nome = new value
    ↓
Compose detects state change
    ↓
Recomposes UI with new value
    ↓
UI updates (field shows text, validation changes)
    ↓
User clicks button
    ↓
onClick triggers → cliques++, resultado = "Hello, $nome!"
    ↓
Compose detects multiple state changes
    ↓
Recomposes UI with new values
    ↓
UI updates (result in green, counter increments)
```

---

## Imperative vs Declarative Approach

### **Imperative Approach (Traditional Android - XML + Java/Kotlin)**

In the **imperative** approach, the programmer **describes HOW** the UI should be updated:

```kotlin
// Imperative example (traditional)
val textView = findViewById<TextView>(R.id.text_resultado)
val button = findViewById<Button>(R.id.button_enviar)

button.setOnClickListener {
    contador++
    textView.text = "Result: $contador"
    textView.setTextColor(Color.GREEN)
    // Multiple method calls to update state
}
```

**Characteristics:**

- ❌ Step-by-step: First do this, then that
- ❌ Direct access to widgets
- ❌ Manual state management between components
- ❌ Prone to synchronization bugs between UI and data
- ❌ More verbose and repetitive code

### **Declarative Approach (Jetpack Compose)**

In the **declarative** approach, the programmer **describes WHAT** the UI should be as a function of state:

```kotlin
// Declarative example (Compose)
var contador by remember { mutableStateOf(0) }

Button(onClick = {
    contador++
}) {
    Text("Click")
}

Text(
    text = "Result: $contador",
    color = if (contador > 0) Color.Green else Color.Black
)
```

**Characteristics:**

- ✅ Descriptive: Defines the desired final state
- ✅ No direct widget access
- ✅ Centralized and reactive state
- ✅ Compose automatically handles synchronization
- ✅ More concise and readable code

### Comparison

| Aspect              | Imperative             | Declarative                |
| ------------------- | ---------------------- | -------------------------- |
| **Focus**           | How to do it           | What to do                 |
| **Updates**         | Manual (call methods)  | Automatic (recomposition)  |
| **Synchronization** | Manual                 | Automatic                  |
| **Readability**     | More complex           | Clearer                    |
| **Errors**          | Easy desynchronization | Guaranteed synchronization |
| **Performance**     | Manual optimization    | Compose optimizes          |

---

## The Role of State in Declarative UI

**State is the single source of truth** in declarative UI:

### 1. **State Defines the UI**

```
State (nome = "John") → UI (shows "Hello, John")
State (nome = "") → UI (shows error, button disabled)
```

### 2. **State Change = Recomposition**

Whenever state changes:

1. Compose detects the change
2. Recomposes the composable (re-executes the function)
3. Compares with previous UI (reconciliation)
4. Applies only necessary changes

### 3. **Automatic Reactivity**

No need for:

- ❌ Explicit listeners for each property
- ❌ Manual observers
- ❌ Setter and getter calls
- ❌ Manual synchronization between data and UI

### 4. **Mini-Challenge Practical Example**

```kotlin
val nomeValido = nome.isNotBlank()  // Derived state
```

This derived state demonstrates the power of declarativeness:

- Validation is **expressed as a function of state**
- The UI automatically uses this state
- When `nome` changes, `nomeValido` is recalculated
- All components that depend on it are recomposed

### 5. **Benefits of Declarative State**

| Benefit             | Impact                                 |
| ------------------- | -------------------------------------- |
| **Predictability**  | UI always matches state                |
| **Testability**     | Just test composable functions         |
| **Maintainability** | UI changes are clear and localized     |
| **Scalability**     | Clear patterns for larger apps         |
| **Performance**     | Selective and optimized recompositions |

---

## How to Run

1. Clone or open the project in Android Studio
2. Sync Gradle dependencies
3. Configure an Android emulator or device
4. Run the application (Run → Run 'app')
5. Interact with the UI:
   - Enter a name
   - See real-time validation
   - Click the button
   - Observe the counter and message

---

## Project Structure

```
ipvc-01-commov/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       │   └── com/example/myapplication/
│   │       │       └── MainActivity.kt
│   │       └── AndroidManifest.xml
│   └── build.gradle.kts
├── build.gradle.kts
├── settings.gradle.kts
└── README.md
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTACT -->

<!-- ACKNOWLEDGMENTS -->

## Acknowledgments

- [Jetpack Compose Documentation](https://developer.android.com/jetpack/compose)
- [Kotlin Documentation](https://kotlinlang.org/docs/home.html)
- [Material Design 3](https://m3.material.io/)
- [Android Developers](https://developer.android.com/)
- [Best README Template](https://github.com/othneildrew/Best-README-Template)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->

[contributors-shield]: https://img.shields.io/github/contributors/03lucasmaciel/ipvc-01-commov.svg?style=for-the-badge
[contributors-url]: https://github.com/03lucasmaciel/ipvc-01-commov/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/03lucasmaciel/ipvc-01-commov.svg?style=for-the-badge
[forks-url]: https://github.com/03lucasmaciel/ipvc-01-commov/network/members
[stars-shield]: https://img.shields.io/github/stars/03lucasmaciel/ipvc-01-commov.svg?style=for-the-badge
[stars-url]: https://github.com/03lucasmaciel/ipvc-01-commov/stargazers
[issues-shield]: https://img.shields.io/github/issues/03lucasmaciel/ipvc-01-commov.svg?style=for-the-badge
[issues-url]: https://github.com/03lucasmaciel/ipvc-01-commov/issues
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/03lucasmaciel
[Kotlin-badge]: https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white
[Kotlin-url]: https://kotlinlang.org/
[Android-badge]: https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white
[Android-url]: https://developer.android.com/
[Compose-badge]: https://img.shields.io/badge/Jetpack%20Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white
[Compose-url]: https://developer.android.com/jetpack/compose
