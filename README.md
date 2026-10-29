# LieBrowser

<p align="center">
  <img src="app/src/forkRelease/res/mipmap-xxxhdpi/ic_launcher.png" width="96" height="96" alt="LieBrowser Logo">
</p>

<p align="center">
  <b>Fast, privacy-focused Android browser based on GeckoView and Fenix without tracking or telemetry.</b>
</p>

---

## 🚀 About the Project

**LieBrowser** is an independent Android fork of Mozilla Firefox (Fenix) and GeckoView, engineered for speed, hardened security, and user privacy.

Unlike upstream Firefox, all intrusive telemetry and analytical pings have been excised, sponsored promotional content is disabled by default, the independent **LieWeb** search engine is preconfigured, and advanced tracking and fingerprinting defenses are enforced at the Gecko engine level.

---

## ⚡ Key Differences from Upstream Firefox

### 1. 🔍 Built-in LieWeb Search (LieSearch)
* Uses the private, independent search engine **LieWeb** (`search.lie2srvv.com`) by default.
* Fast search autocompletion via API without transmitting user IDs, advertising beacons, or browsing history to third-party ad networks.

### 2. 🛡️ Complete Telemetry & Tracking Elimination
* Built-in telemetry dispatchers deactivated: `toolkit.telemetry.enabled = false`, `toolkit.telemetry.unified = false`.
* Remote Nimbus experiments and telemetry probes permanently disabled (`experiments.supported = false`).
* Performance telemetry, Glean metric uploads, and diagnostic tracking calls eliminated.

### 3. 🔒 Hardened Gecko Engine Privacy Defaults
* **Total Cookie Protection (dFPI):** Per-domain cookie isolation (`network.cookie.cookieBehavior = 5`) blocking cross-site tracking across the web.
* **WebRTC IP Leak Prevention:** Hides the local device IP address during WebRTC negotiations (`media.peerconnection.ice.no_host = true`).
* **Fingerprinting & Cryptomining Defense:** Active protection against device fingerprinting scripts (`privacy.trackingprotection.fingerprinting.enabled = true`) and background cryptominers.
* **DNS Prefetch Suppression:** Prevents background DNS resolution of links before user interaction (`network.dns.disablePrefetch = true`, `network.prefetch-next = false`).
* **Seamless VPN Compatibility:** DNS-over-HTTPS does not hijack system DNS by default, ensuring external VPN routing and custom tunnels function without conflict.

### 4. 🧹 Clean, Ad-Free Homepage
* Pocket recommendation blocks and sponsored articles removed.
* Sponsored search suggestions disabled.
* Mozilla VPN and third-party upsell banners removed from menus and settings.
* Preconfigured quick shortcuts to Lie ecosystem services (`vpn.lie2srvv.com`, `cord.lie2srvv.com`, `mail.lie2srvv.com`).

### 5. 🧩 Extended Add-on Support & `about:config`
* Full access to `about:config` for granular browser engine tuning on mobile.
* Support for a wide variety of desktop and mobile extensions (uBlock Origin, Dark Reader, etc.) with support for installing local `.xpi` files.

---

## 📦 Building from Source

### Prerequisites
* **JDK 17+**
* **Android SDK** (API Level 34+, build-tools 34.0.0+)
* `ANDROID_HOME` or `ANDROID_SDK_ROOT` environment variable configured

### Build Instructions

```bash
# Clone the repository
git clone https://github.com/lie2srvv/LieBrowser.git
cd LieBrowser

# Build Release APK (arm64-v8a, armeabi-v7a, x86_64)
./gradlew app:assembleForkRelease

# The generated APKs will be located in:
# gradle/build/app/outputs/apk/forkRelease/
```

### Signing the APK

```bash
apksigner sign --ks ~/.android/debug.keystore \
  --ks-pass pass:android \
  --ks-key-alias androiddebugkey \
  --key-pass pass:android \
  --out LieBrowser-arm64.apk \
  gradle/build/app/outputs/apk/forkRelease/app-arm64-v8a-forkRelease-unsigned.apk
```

---

## 📄 License

This project is licensed under the **Mozilla Public License 2.0 (MPL-2.0)**.
See the `LICENSE` file or visit http://mozilla.org/MPL/2.0/ for details.
