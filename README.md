[![](https://jitpack.io/v/ReemMousaES/es-ptp-camera.svg)](https://jitpack.io/#ReemMousaES/es-ptp-camera)
# ES PTP Camera

Android library for communicating with digital cameras via USB using the Picture Transfer Protocol (PTP).

## Features

- **Nikon Camera Support**: Remote control, live view, capture, focus, settings
- **Canon EOS Support**: Remote control, live view, capture, bulb mode
- **USB Host API**: Direct USB communication with cameras
- **Live View Streaming**: Real-time preview from supported cameras
- **Camera Settings**: Control ISO, aperture, shutter speed, white balance, and more

## Installation

Add JitPack repository to your project's `build.gradle` (project level):

```kotlin
allprojects {
    repositories {
        maven { url = uri("https://jitpack.io") }
    }
}
```

Add dependency to your app's `build.gradle`:

```kotlin
implementation("com.github.YOUR_USERNAME:es-ptp-camera:1.0.0")
```

## Usage

### Initialize PTP Service

```kotlin
val ptpService = PtpUsbService(context)
ptpService.addPtpServiceListener(object : PtpService.PtpServiceListener {
    override fun onCameraConnected(camera: Camera) {
        // Camera connected and ready
    }

    override fun onCameraDisconnected() {
        // Camera disconnected
    }

    override fun onError(error: PtpError) {
        // Handle error
    }
})
ptpService.startService()
```

### Capture Photo

```kotlin
camera.initiateCapture(object : PtpAction.Callback {
    override fun onSuccess() {
        // Capture successful
    }

    override fun onError(error: PtpError) {
        // Handle error
    }
})
```

### Live View

```kotlin
// Start live view (Nikon)
camera as NikonCamera
camera.startLiveView()

// Get live view image
camera.getLiveViewImage { data ->
    // Process live view frame
}

// Stop live view
camera.stopLiveView()
```

### Get Device Properties

```kotlin
camera.getDevicePropValue(PtpConstants.DEVICE_PROP_EXPOSURE_PROGRAM) { value ->
    // Handle property value
}
```

## Requirements

- Min SDK: 24 (Android 7.0)
- Target SDK: 35
- Android device with USB Host support

## Permissions

Add to your `AndroidManifest.xml`:

```xml
<uses-feature android:name="android.hardware.usb.host" />
```

## Attribution

This library is a fork of the original [RemoteYourCam USB](https://github.com/michaelzoech/remoteyourcam-usb) project by:

- Nils Assbeck
- Guersel Ayaz
- Michael Zoech

Licensed under Apache License 2.0.

## License

```
Copyright 2013 Nils Assbeck, Guersel Ayaz and Michael Zoech
Copyright 2024 ExtremeSolution

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
```

See [LICENSE](LICENSE) for full license text.
