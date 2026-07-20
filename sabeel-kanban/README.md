# Sabeel Institute Kanban — public download page

The app itself lives in a **private** repo (`faisal-shah/sabeel-institute-kanban`).
This directory exists only so the team can download the Android build without a
GitHub account: releases on a private repo are not publicly downloadable, and
GitHub Pages bandwidth is free.

## Updating — keep the APK in its OWN commit

Only the arm64 build is published here. Anyone on a 32-bit device can be sent
the APK from the private repo's release; it is not worth a permanent 24 MB in
this history for a case that may never come up.

```sh
R=../../sabeel-institute-kanban/app/android/app/build/outputs/apk/release
cp "$R/app-arm64-v8a-release.apk" sabeel-kanban/sabeel-kanban-arm64-v8a.apk

git commit -m "..." -- sabeel-kanban/index.html   # page and version, text only
git commit -m "APK v0.x.y (binary)" -- sabeel-kanban/sabeel-kanban-arm64-v8a.apk
```

**Never mix the binary with text changes in one commit.** Keeping each APK
alone in its own commit is what makes the history reclaimable: those commits can
be dropped with an interactive rebase or filter and force-pushed, without losing
any of the page's real history. Mixing them means rewriting would take the page
edits with it.

## The cost, so it is not a surprise later

Every build adds ~30 MB to git history **permanently** — overwriting the file
does not reclaim the old blob. Roughly thirty builds before GitHub starts
warning around 1 GB.

Because each APK sits alone in its own commit, reclaiming the space is
straightforward when the time comes: drop the old APK commits and force-push.
Keep the most recent one.

```sh
git rebase -i <before-the-first-apk-commit>   # drop the old "APK ... (binary)" commits
git push --force-with-lease
```

`--force-with-lease` rather than `--force`: it refuses if someone else has
pushed in the meantime, which is the whole difference between rewriting your own
history and destroying somebody else's.

## What is in the APK

Nothing secret. The Firebase web config is public by design, the Sentry DSN is
send-only, and access is gated by `@oursabeel.com` sign-in plus admin approval —
so a stranger downloading this cannot see any data. The build is signed with the
Android **debug** keystore; that is fine for direct distribution but is tracked
in the private repo's `TODO.md` § F.
