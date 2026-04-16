# tanvrit-sdk · auth

> Authentication flows: phone OTP, WhatsApp OTP, email magic link, social login (Google / Apple / Facebook), passkeys, and MPIN.

[![Maven](https://img.shields.io/badge/maven.tanvrit.com-1.0.12-blue)](https://maven.tanvrit.com)
![KMP](https://img.shields.io/badge/Kotlin_Multiplatform-7_targets-blueviolet)

## Install

### Option A — Tanvrit Gradle plugin _(recommended)_

```kotlin
// settings.gradle.kts
pluginManagement {
    repositories { maven { url = uri("https://maven.tanvrit.com") } }
}
```

```kotlin
// build.gradle.kts
plugins { id("com.tanvrit.sdk") version "1.0.12" }

tanvrit {
    version = "1.0.12"
    modules = listOf("auth")
}
```

### Option B — Direct dependency

```kotlin
// settings.gradle.kts
dependencyResolutionManagement {
    repositories { maven { url = uri("https://maven.tanvrit.com") } }
}
```

```kotlin
// build.gradle.kts  (KMP)
kotlin {
    sourceSets {
        commonMain.dependencies {
            implementation("com.tanvrit:auth:1.0.12")
        }
    }
}
```

## Targets

| Platform | Artifact |
|----------|----------|
| Android | `auth-android` |
| Iosarm64 | `auth-iosarm64` |
| Iossimulatorarm64 | `auth-iossimulatorarm64` |
| Iosx64 | `auth-iosx64` |
| Jvm | `auth-jvm` |
| Js | `auth-js` |
| Wasm Js | `auth-wasm-js` |

## Quick start

```kotlin
val auth = AuthHandler.shared()

// Phone OTP
auth.sendOtp(dialCode = "+91", mobile = "9876543210") { success ->
    if (success) showOtpScreen()
}

// Verify OTP
auth.verifyOtp(otp = "123456") { response ->
    if (response?.isNewUser == true) showNameScreen()
    else navigateHome()
}

// Check auth state
auth.authState.collect { state ->
    when (state) {
        is AuthState.Authenticated -> navigateHome()
        is AuthState.Guest         -> showAuthScreen()
        is AuthState.Loading       -> showSpinner()
    }
}
```

## Resources

- **Full SDK source:** [tanvrit/sdk](https://github.com/tanvrit/sdk)
- **All modules:** [maven.tanvrit.com](https://maven.tanvrit.com)
- **Issues:** [tanvrit/sdk/issues](https://github.com/tanvrit/sdk/issues)
