# LUBM AI Workshop — Lessons Learned

<!-- Format for each entry:

## [DATE] — [SHORT TITLE]
**Problem:** What went wrong
**Root Cause:** Why it happened
**Fix:** What was done to resolve it
**Prevention:** What is now baked into the workflow to prevent recurrence
**Affects:** Which files/scripts/rules were updated

-->

## 2026-03-26 — MP4 video on Vercel requires explicit Content-Type header
**Problem:** Video may not play on Vercel even if it works locally
**Root Cause:** Vercel CDN may not serve correct video/mp4 MIME type without explicit header declaration
**Fix:** Added Content-Type: video/mp4 header in vercel.json for /assets/video/*.mp4
**Prevention:** Always declare Content-Type header for mp4 files in vercel.json on every project
**Affects:** vercel.json

## 2026-03-27 — Slide 2 video controls
**Problem:** Video played but had no sound and no user controls
**Root Cause:** Browser autoplay policy requires muted attribute for autoplay — sound cannot play without user interaction. No controls were visible to the user.
**Fix:** Added prominent play/pause (72px gold circle), mute/unmute (56px gold circle), progress bar with scrubbing, and fullscreen button. Sound off badge shown at top until user unmutes. On unmute click, video.muted = false triggers sound after user interaction — browser allows this.
**Prevention:** Every video slide in every DigitAlchemy® deck must have visible play/pause and mute/unmute controls. Never rely on browser default controls or assume sound will play on load.
**Affects:** index.html
