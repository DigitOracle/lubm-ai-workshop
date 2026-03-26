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
