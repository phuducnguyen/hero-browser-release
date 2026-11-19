# Hero Browser — installers

Hero Browser is an anti-detect browser for teams that run many accounts. Every profile is its own
device: the operating system a site sees, a screen and GPU, fonts, language and time zone, and its
own proxy, cookies and storage. Nothing is shared between profiles.

This repository holds the installers, the HeroFox engine builds and `latest.json`, the feed the app
reads to update itself. The source code is not public.

## Download

The latest stable release for Windows 10 and 11, x64:

**https://github.com/phuducnguyen/hero-browser-release/releases/latest**

Run `Hero-Browser-<version>-x64-setup.exe`. Windows SmartScreen shows *Windows protected your PC*
because the installer carries no code-signing certificate yet: choose **More info**, then
**Run anyway**. On first start the app downloads the browser engine (about 150 MB) and the device
library, so it needs an internet connection once.

To check the file, compare its SHA-256 with the one in the release notes:

```
certutil -hashfile Hero-Browser-<version>-x64-setup.exe SHA256
```

Hero Browser keeps its data in `%APPDATA%\hero-browser\`. Installing a newer version over an older
one keeps profiles, proxies, bookmarks and settings.

## Updates

From **0.9.0** the app updates itself: a new release downloads in the background, and
**Restart to update** installs it and reopens the app. Browsers that are open stay open, and the
restarted app takes them over again.

- `latest.json` on the release marked *latest* is the feed; installed apps read
  `releases/latest/download/latest.json`.
- Every installer is signed with Hero Browser's minisign key and an unsigned one is refused.
- Versions up to 0.8.1 cannot update themselves. Install 0.9.0 by hand once; releases after it
  arrive through the app.
- Settings → General → *Download updates automatically* turns the background download off.

## Releases

Every release has its own notes: what changed, upgrade notes, known issues, the installer's
SHA-256 and the checks that ran before publishing. `engine-firefox-*` releases are the HeroFox
engine (Camoufox, MPL-2.0, repackaged by Hero Browser), which the app downloads from here.

## Licence

The launcher is MIT. HeroFox is Camoufox by daijro and contributors, under the Mozilla Public
License 2.0. The HeroChrome engine is a separate, closed-source patched Chromium distributed by
its authors under their own terms; Hero Browser downloads it, it is not part of these releases.
