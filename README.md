<h1 align="center">Aliucord</h1>
<p align= "center">
  <a href="https://discord.gg/EsNDvBaHVU">
    <img alt="Discord" src="https://img.shields.io/discord/811255666990907402?color=%2300C853&label=Support%20Server&logo=discord&logoColor=%2300C853&style=for-the-badge">
  </a>
</p>

Aliucord is a modification for the Android Discord app inspired by desktop client modifications.

Unlike other Android Discord app modifications, you don't need to rebuild the APK when adding or removing plugins, because Aliucord hooks at runtime using the [Pine](https://github.com/canyie/pine) java method hook framework.

## Table of contents

- [Important Information](#important-information)
  - [Supported Architectures](#supported-architectures)
  - [Supported Android version(s)](#supported-android-versions)
  - [Supported Discord version(s)](#supported-discord-versions)
- [Installation](#installation)
- [Plugin Installation](#plugin-installation)
  - [Troubleshooting](#troubleshooting)
- [Building from source](#building-from-source)
  - [Porting Aliucord to the latest Discord version](#porting-aliucord-to-the-latest-discord-version)

## Important Information

### Supported Architectures

- arm
- arm64

This is due to pine only supporting `arm` and `arm64`. Thus Aliucord will not work on x86_64 or similar architectures. This means that it will not work in most desktop emulators

### Supported Android version(s)

- 7.0+ (SDK 24+)

### Supported Discord version(s)

- 81.1 - Alpha (81100)

## Installation

1. Download and install [Installer-release.apk](https://github.com/Aliucord/Aliucord/raw/builds/Installer-release.apk) from the `builds` branch
2. Open the newly installed "Aliucord Installer" app from your app drawer
3. Click "Install", then choose the "Download" option
    - *psst... only choose the other options if you know what you're doing!*
5. Wait for it to finish patching the Discord APK
6. Click "Install" once prompted by Android and wait for Aliucord to finish installing
7. If Google Play warns you about this application being unverified, ignore it as it triggers thanks to an unverified signature¹
8. Open Aliucord, grant access to files (it needs this for finding plugins), log in to your account, and voila! Aliucord is at your fingertips!

> ¹ If you'd like, you can disable this warning by turning off Play Protect in Google Play's settings, it's mostly useless.
> 
> Play Protect can be turned off by tapping on your user icon in the top right of Google Play, tapping on "Play Protect," tapping on the cog icon in the top right, and finally toggling "Scan apps with Play Protect" to off. This may result in Google Play "nagging" you to re-enable it sometimes when sideloading apps.*


## Plugin Installation

1. Open your preferred file manager
2. Navigate to your internal storage (likely `/storage/emulated/0/` or `/sdcard/`)
3. Look for the folder named "Aliucord" and open it
4. Open the "plugins" folder, or if it doesn't exist, create it yourself. Remember: LOWERCASE "p"
5. Either search GitHub or join our [support server](https://discord.gg/EsNDvBaHVU) and visit the `#plugin-links` channel for plugins to download
6. Visit the `builds` branch of any GitHub repositories you get linked to and download the ZIP files of the plugins you wish to load with Aliucord
7. Once you've downloaded the plugins, move them into the `Aliucord/plugins` folder
8. Open Aliucord, check the plugins tab and hopefully see your plugin(s) listed!

> Hint: There is a [PluginDownloader plugin](https://github.com/Vendicated/AliucordPlugins/blob/builds/PluginDownloader.zip?raw=true) that makes installing plugins a lot easier by adding download buttons to messages in either of the plugin channels


### Troubleshooting

- Try closing and then reopening Aliucord
- Double check that Aliucord has permission to access files
- Reinstall Aliucord, making sure to use the "Download" option

...and if none of these work, please visit our [support server](https://discord.gg/EsNDvBaHVU) and go to `#support` for help!


## Building from source
See `.github/workflows/build.yml` for all build steps.

## Porting Aliucord to the latest Discord version

1. Acquire the version of the Discord APK you'd like to port Aliucord to
2. Decompile it using [Apktool](https://github.com/iBotPeaches/Apktool)
    - e.g `apktool d discord-n.apk` (replace n with build number)
3. Apply `manifest.patch` to the `AndroidManifest.xml` file
4. Rebuild the Discord APK using Apktool
    - e.g `apktool b discord-n.apk` (replace n with build number)
5. Copy `build/apk/AndroidManifest.xml` to `.assets/AndroidManifest.xml` and to `Aliucord/AndroidManifest.xml` on your Android device
6. Build Aliucord using [buildtool](https://github.com/Aliucord/buildtool) and copy to `Aliucord/Aliucord.dex` on your Android device
7. Open Aliucord Installer, open the app settings, clear cache, and enable "Use Aliucord.dex from storage"
8. Install Aliucord
9. Ensure you've got a `logcat` catcher ready to go
10. Open Aliucord and fix any errors that show in `logcat`
