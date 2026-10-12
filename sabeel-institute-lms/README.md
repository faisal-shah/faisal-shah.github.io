# Sabeel Institute LMS — public download page

The app's source is the public repo `Sabeel-Institute/lms`. This page is where
students and staff get the Android build; the app's update screen and its
`/get-app` page both link here (`DOWNLOAD_PAGE_URL` in `@sabeel/shared`).

It replaces `../sabeel-recording-app/` on switchover day, when the institute
moves from Sabeel Class Recordings to this app. Until then the page says the app
is not released yet and is not listed on the site's index.

## What's committed here

- `index.html` — the download page.

The **APKs are not committed here**: they are assets on the GitHub Release for
each version tag of `Sabeel-Institute/lms`, under unversioned names, so the
links below always resolve to the newest release:

```
https://github.com/Sabeel-Institute/lms/releases/latest/download/sabeel-institute-lms-arm64-v8a.apk
https://github.com/Sabeel-Institute/lms/releases/latest/download/sabeel-institute-lms-universal.apk
```

The page carries the version number and what changed.

## Note

Two sign-in populations: **students** use an email/password account their teacher
creates (they set the password from an emailed link); **staff** use Google
sign-in restricted to the institute's domain, gated by admin approval. The page
links to the app, never to a way of getting an account: the Android app's
store exemption depends on that (see the app repo's `CLAUDE.md`).
