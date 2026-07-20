# Sabeel Time Tracker — public download page

The app lives in a **private** repo (`faisal-shah/sabeel-institute-time-tracker`).
This directory exists so the team can download the Android build without a
GitHub account: releases on a private repo are not publicly downloadable, and
Pages bandwidth is free.

Same arrangement as `../sabeel-kanban/`.

## Updating — keep the APK in its OWN commit

Take the APK from the **release**, not a local build: the release is the artifact
that was actually tested and published.

```sh
cd ../sabeel-institute-time-tracker
gh release download <tag> --pattern '*arm64.apk' --pattern 'USER-MANUAL.pdf' \
  --dir ../faisal-shah.github.io/sabeel-time-tracker --clobber
cd ../faisal-shah.github.io
mv sabeel-time-tracker/sabeel-time-tracker-*-arm64.apk \
   sabeel-time-tracker/sabeel-time-tracker-arm64-v8a.apk

git commit -m "..." -- sabeel-time-tracker/index.html      # page + version, text only
git commit -m "APK <tag> (binary)" -- sabeel-time-tracker/sabeel-time-tracker-arm64-v8a.apk
```

The filename is deliberately unversioned so the link never goes stale; the page
carries the version instead.

**Never mix the binary with text changes in one commit.** Keeping each APK alone
is what makes the history reclaimable later — those commits can be dropped and
force-pushed without taking the page's real history with them.

## Cost

~38 MB per published build, permanently, since overwriting does not reclaim the
old blob. Combined with the kanban page that is roughly 68 MB per round of
updates to both. When it matters:

```sh
git rebase -i <before-the-first-apk-commit>   # drop old "APK ... (binary)" commits
git push --force-with-lease
```

## Note

Unlike the kanban app, this one has **no email-domain restriction** — any Google
account can sign in, and access is controlled entirely by admin approval. The
page copy says so; do not copy the kanban wording over it.
