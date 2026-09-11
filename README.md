# DarkRoute for Android

The private swap router as an Android app. A signed shell around the same web app you get at
[app.darkroute.exchange](https://app.darkroute.exchange): quote a private route, get the one-time
deposit address, track the order. The venue is named, the fee is printed, no keys are held.

This repository holds the README and the signed builds under **Releases**. Nothing else.

## Download

Latest build: see [Releases](../../releases). The same file is served at
[darkroute.exchange/android](https://darkroute.exchange/android) with its hash printed next to it.

| | |
|---|---|
| Package | `exchange.darkroute.app` |
| Android | 7.0 (API 24) and up, targets API 36 |
| Permissions | one: `INTERNET` |
| Size | about 3.6 MB |
| Play Store | not yet. Until the listing exists, the APK in Releases is the release. |

## Verify before you install

An APK from a project account is exactly the kind of file you should not trust blindly. Two checks:

1. **File hash.** Each release lists the sha256 of its APK. Compare with the file you downloaded
   (`shasum -a 256 darkroute-android-*.apk` on a computer, or any checksum app on the phone).
2. **Signing certificate.** Every DarkRoute build is signed with the same certificate:

   ```
   SHA-256: D3:A6:D8:43:C6:1A:5D:7C:6A:7E:8E:8A:93:32:45:92:7D:B1:BF:46:E4:1B:CB:14:A2:BB:40:8B:76:8A:90:07
   ```

   The same fingerprint is published at
   [app.darkroute.exchange/.well-known/assetlinks.json](https://app.darkroute.exchange/.well-known/assetlinks.json),
   which is how Android decides that order links may open in this app. A repacked APK cannot carry it.
   Check with `apksigner verify --print-certs darkroute-android-*.apk`.

## Install

1. Download the APK from Releases.
2. Open it. Android asks you to allow installs from your browser for this one file; that is the
   normal path for an app outside the Play Store.
3. Open DarkRoute. The swap card loads from the router. Offline you get one retry page, nothing else.

## What it does not do

- It does not collect analytics or telemetry. No SDKs, no crash reporter, no advertising id.
- It does not hold keys. Deposits go from your own wallet or exchange to the address on the order
  page. "Send with wallet" inside the app is limited for now, because a WebView has no browser
  wallet; use the address and amount shown, or open the pay link in a browser that has your wallet.
- It does not talk to anything but `app.darkroute.exchange`.

## Source

The shell is a small Capacitor project (a manifest, a theme, a config that points at the app).
Its source is not public yet. The web app it loads is the same one every browser gets; the Chrome
extension source is public at [darkrouteRH/extension](https://github.com/darkrouteRH/extension).

## Links

- Website: https://darkroute.exchange
- App: https://app.darkroute.exchange
- Android page, with hash: https://darkroute.exchange/android
- X: https://x.com/DarkrouteRH

## License

The builds are distributed as is, without warranty. DarkRoute is a non-custodial routing interface;
it does not hold user funds and does not guarantee execution, rates or settlement times.
