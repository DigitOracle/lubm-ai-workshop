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

## 2026-03-27 — Unmute click changes icon but no sound plays
**Problem:** Clicking unmute changes the icon correctly but audio does not play
**Root Cause:** Setting video.muted = false alone does not unlock browser audio. The browser requires video.play() to be called explicitly within the same user gesture (click handler) to grant audio permission. Without play(), the video remains silent even when muted = false.
**Fix:** Call v.play() inside the unmute branch of the click handler, immediately after setting v.muted = false. Wrap in promise .then()/.catch() to handle browsers that still block.
**Prevention:** Any time you unmute a video programmatically, always call play() in the same synchronous user gesture. Never rely on muted = false alone.
**Affects:** index.html, LESSONS_LEARNED.md

## 2026-03-27 — Chrome blocks audio even after unmute click on new sites
**Problem:** Clicking unmute changes icon but no sound plays on new/low-traffic Vercel domain
**Root Cause:** Chrome's Media Engagement Index (MEI) is zero for new sites. Even with a user click on the unmute button, Chrome still blocks audio on sites with no engagement history. This is a second layer of audio blocking beyond the basic autoplay policy.
**Fix:** Added a full-screen splash/entry screen. The "Enter Workshop" button click satisfies Chrome's MEI user-gesture requirement for the entire session. All subsequent video audio (including unmute) works correctly after this initial interaction.
**Prevention:** Every DigitAlchemy® deck with video audio must have a splash entry screen. Never expect audio to work without a full-page initial user interaction. This is the pattern used by YouTube, Netflix, and all major video platforms.
**Affects:** index.html, LESSONS_LEARNED.md
