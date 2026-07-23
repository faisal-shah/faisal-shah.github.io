# Sabeel Class Recordings — public download page

The app lives in a **private** repo (`faisal-shah/sabeel-recording-app`). This
directory exists so students and staff can download the Android build without a
GitHub account: releases on a private repo are not publicly downloadable, and
Pages bandwidth is free.

Same arrangement as `../sabeel-time-tracker/` and `../sabeel-kanban/`.

## What's committed here

- `index.html` — the download page (web app, Android APK, user manual).
- `USER-MANUAL.pdf` — the manual, committed so the page can serve it directly.

The **APKs are NOT committed** — they're assets on the `recording-latest`
GitHub Release of *this* pages repo (see `.gitignore`, which blocks `*.apk`).
Committing per-build APKs bloats history and has to be rewritten out later.

## Updating

Rebuild the manual and APKs in the source repo, then:

```sh
# 1. Refresh the committed manual (text/PDF only)
cp ../../sabeel-recording-app/docs/USER-MANUAL.pdf USER-MANUAL.pdf
git commit -m "Recording app: refresh user manual" -- sabeel-recording-app/

# 2. Replace the release assets (APKs live on the release, not in git)
REL=../../sabeel-recording-app/app/android/app/build/outputs/apk/release
gh release upload recording-latest \
  "$REL/app-arm64-v8a-release.apk#sabeel-recording-app-arm64-v8a.apk" \
  "$REL/app-universal-release.apk#sabeel-recording-app-universal.apk" \
  --clobber -R faisal-shah/faisal-shah.github.io
```

The APK filenames are deliberately unversioned so the download link never goes
stale; the page carries the version number instead.

## Note

Two sign-in populations: **students** use an email/password account their teacher
creates (they set the password from an emailed link); **staff** use Google
sign-in restricted to the institute's domain, gated by admin approval. The page
copy reflects this — don't copy the time-tracker or kanban wording over it.
