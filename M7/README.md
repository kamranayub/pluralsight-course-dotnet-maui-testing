# Distributing to Google Play

## Prerequisites

- Android SDK
- OpenJDK
- Compatible Android device

Follow the [Getting Started documentation](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation) for Android.

### Installing OpenJDK 17

I followed the instructions for [installing OpenJDK on macOS](https://learn.microsoft.com/en-us/java/openjdk/install).

After it was installed, I had to set my `JAVA_HOME` environment variable:

```sh
export JAVA_HOME="/Library/Java/JavaVirtualMachines/microsoft-17.jdk/Contents/Home"
```

### Installing the Android SDK

I was not able to get the recommended `InstallAndroidDependencies` [build target](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-9.0&tabs=visual-studio-code#using-the-installandroiddependencies-target) to work on my Mac M1. It was throwing a null reference exception for `path1`.

Instead I installed the Android SDK through [Android Studio](https://developer.android.com/studio/install).

**`ANDROID_HOME` must be set**

After installing Android Studio, I needed to set my `ANDROID_HOME` environment variable.

```sh
export ANDROID_HOME="/Users/myuser/Library/Android/sdk"
```

> [!NOTE]
> If you install the SDK via Android Studio on macOS, the SDK will be located in `~/Library/Android/sdk`

**Verifying Android Environment**

To test your Android environment, in Visual Studio Code with the .NET MAUI extension, go to **Command Palette -> .NET MAUI: Configure Android -> Refresh Android Environment**.

The output window should print out all the required SDK tools required.

**Additional SDK packages were needed**

My Android Studio installation did not include the `cmdline-tools` or `build-tools` package by default. You can follow the instructions to install via `sdkmanager` or use the [Android Studio SDK Manager GUI](https://developer.android.com/studio/intro/update#sdk-manager).

This is the output from my MAUI environment on my Mac M1:

```
✓ platforms/android-35 - INSTALLED (version '2')
✓ build-tools/35.0.0 - INSTALLED (version '35.0.0')
✓ platform-tools - INSTALLED (version '35.0.2')
✓ cmdline-tools/12.0 - INSTALLED (version '17.0')
```

**Android Emulator**

I ran the installation commands shown in the MAUI docs under [Install an Android Emulator](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-9.0&tabs=visual-studio-code#download-and-install-an-android-emulator).

However, I was getting the following error trying to run the app on the emulator:

> Selected device not running.

With Android Studio, it looks like you need to start the emulator in the UI, or use the Terminal:

In the `$ANDROID_HOME/emulator` directory:

```sh
./emulator -avd MyAndroidVirtualDevice-API35
```

This will launch the emulator and power it up in a standalone window.

After that, VS Code was able to deploy the app to the emulator.

**Setting up physical device**

I have a Google Pixel 6. After enabling Developer Mode, my USB port was not working for USB debugging so I opted to [use wireless debugging](https://developer.android.com/studio/run/device#wireless).

Once you pair the device, it will be available as a Debug Target in Visual Studio Code.

> [!WARNING]
> I was running into an issue where the app would crash on startup after debugging. It seems like you cannot be running the Android emulator while debugging on a physical device. Once I quit the emulator and powered it off, the physical device debugging started to work.