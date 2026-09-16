---
name: phd-case-poster-batch
description: Manually batch-process PhD outreach email, interview invitation, and offer screenshots into 乐意轻学 branded posters. Use only when the user explicitly asks to process images from a user-specified folder (or a named test subfolder), classify screenshots as 套磁回复/面试邀请/Offer, select the green/purple/blue template, verify current university rankings, mosaic personal data, preserve each input filename exactly, archive finished posters in a YYYY-MM-DD folder, and KEEP the original screenshots in place (never delete or move them). Do not schedule or monitor automatically.
---

# 博士案例海报批处理

Read [references/template-rules.md](references/template-rules.md) completely before processing images.

## Usage briefing (MUST tell the user before every run)

Before doing anything, briefly explain to the user how this run will work, in plain language:

1. **Input folder**: ask the user which folder holds the screenshots (or confirm the folder from the previous run).
2. **Output**: posters are saved inside that folder under a `YYYY-MM-DD` subfolder (today's date), keeping the original filenames exactly.
3. **Flow**: each screenshot is read and classified (普通回复 → green / 面试邀请 → purple / Offer → blue), the latest QS/USNEWS ranking is verified online, then each poster is built on the Ardot canvas with the approved style and exported as PNG.
4. **Privacy**: all personal/sensitive info (names, emails, signatures, research topics) is covered with gray mosaic blocks; key sentences are outlined in red. Nothing sensitive is ever shown in the report.
5. **Original files are KEPT**: source screenshots are never deleted or moved — they stay in the input folder. Posters are saved separately in the `YYYY-MM-DD` output folder.
6. **First-time tip**: for a brand-new environment/colleague, recommend running 1-2 test images first to confirm font rendering before batch processing.

## Fixed locations

- Inbox: the **user-specified input folder**. Ask the user for the folder path at the start of each run (or reuse the folder from the previous run if unchanged). Never hard-code any specific user's desktop path — this skill may be shared with other colleagues.
- Run only after the user explicitly asks. Never create a timer, recurring automation, watcher, or background monitor for this workflow.
- Treat supported image files placed directly in the inbox as unprocessed inputs.
- If the user explicitly names or approves a test subfolder, treat supported image files directly inside that one subfolder as the current batch inputs.
- Otherwise ignore `.DS_Store`, hidden files, and all subfolders; dated subfolders are outputs, not inputs.
- Style source: follow the design spec in [references/template-rules.md](references/template-rules.md) (2026-08 年轻互联网版). The old template images were removed from the repo.
- Known Ardot pitfall (IMPORTANT for stable reproduction): creating poster frames by Copying a sample frame can render with stale/wrong content (screenshots/exports show other posters' Hero text) even though node data is correct — observed when two frames' contents appeared swapped. **Stable, reproducible workflow:**
  1. Create a FRESH Ardot design file for each batch (never reuse a file that has shown rendering issues).
  2. Build every poster from scratch with Insert (I) operations only — do NOT Copy the sample frame. Use the exact parameter tables in `references/template-rules.md`.
  3. Build all frames before exporting; verify content by reading node data, then export PNG at scale=1 and do a pixel-diff sanity check against a known-good reference (same-content frames should differ <5%, different-content frames should differ >8%).
  4. If a file starts rendering mixed content, abandon it and start a new file.

## Process each input

1. Record the exact filename, including capitalization, punctuation, spaces, Chinese characters, and extension. Never rename it.
2. Inspect and transcribe only visible screenshot content. Use the filename only as a hint and output identifier.
   - **Same thread split across multiple screenshots** (e.g. `Xxx University.png` + `Xxx University2.png`, or a first message inviting a meeting plus a later message confirming the time/room): merge them into **one** poster for that student+school — combine the earlier invitation and the later confirmation so the poster shows the complete outcome. Name the merged output after the first screenshot's filename. Tell the user in the report which files were merged.
   - **User annotations inside a filename** (e.g. `陈佳昕Universitat Pompeu Fabra（不是面试不要搞错）.jpg`) are instructions to the assistant, not part of the real name — drop the bracketed note from the output filename, keep the rest exact, and state this in the report.
3. Resolve conflicts in favor of the screenshot: school, country/region, content type, and facts visible in the screenshot override the filename and user-supplied labels.
4. Classify before choosing a template:
   - formal admission or conditional/unconditional offer → blue Offer;
   - explicit interview, meeting, Zoom, Teams, or further-conversation invitation → purple interview;
   - ordinary reply, material request, process guidance, research/funding discussion, or supervision possibility without a meeting invitation → green outreach reply.
   - **Conditional / future-tense meetings are NOT interview invitations.** If the professor only says a meeting may happen *after* a prerequisite (e.g. "Before deciding whether to support your candidacy, I would kindly ask you to provide a writing sample. **After that, we can arrange an online meeting.**" or "After that, we can arrange a short meeting with Dr X to discuss the next steps"), this is a **green ordinary reply** — the meeting is not yet agreed. Purple requires a real invitation: a proposed/confirmed time slot, a requested availability, or a stated willingness to meet ("I would be happy to meet with you", "let's find a time", "Are you free on ...?"). When in doubt, ask the user — a wrongly-purple poster misrepresents the case.
   - When multiple classes are explicit, use Offer > interview > ordinary reply.
5. Identify the school from screenshot evidence. Verify the latest public ranking immediately before generation:
   - United States: latest U.S. News Best Global Universities rank; label `学校中文名｜USNEWS数字`.
   - Other countries/regions: latest QS World University Rankings; label `学校中文名｜QS数字`.
   - Show the ranking only when the numeric rank is 200 or better. If the rank is greater than 200, or the entire published ranking band begins after 200, show only the Chinese school name.
   - Do not include ranking year, “世界大学排名”, or “第”.
   - **Translate the school name COMPLETELY — including any place name attached to it.** An English school name whose trailing part is a state/province/city must be translated too, not left in English. E.g. `Queen's University, Ontario` → `女王大学(安大略)` (NOT `女王大学`), `University of California, Berkeley` → `加州大学伯克利分校`. Never output a half-translated label like `女王大学 Ontario`.
   - For Sino-foreign joint-venture universities, use `中外合办-PHD` as the title region; do not use `中国-PHD`.
6. Generate a branded poster on the Ardot canvas following the layout, color, type, watermark, and mosaic rules in [references/template-rules.md](references/template-rules.md). Use the type/color mapping (green/purple/blue) from the classification. Then export the poster frame as PNG.
   - Non-screenshot inputs are handled too: a **PDF admission letter** = blue Offer template (`博士OFFER来啦!`); render it with `pymupdf` to read it, omit `DearRow` when the letter has no salutation, put program / commencement date / duration / tuition in the red box, and save the poster as the original PDF name with a `.png` extension. The PDF itself is kept untouched.
   - **The content bubble (ContentCard) height is FIXED — never `hug_contents`.** A short email must NOT shrink the bubble; the extra space simply stays blank at the bottom. This keeps every poster visually consistent. Nominal full height = **870** (bubble bottom y=1340, gap 42 to the slogan at y=1382); the 李晨瑞-MSU reference poster happens to sit at **877** (bottom y=1347) — the 7px difference is not visible. **Within one batch always use the exact same value.** When repairing an existing batch, read the height the batch's other posters already use and reuse it (e.g. 9-7补 → 877, 9-11 → 870). If you notice an already-built poster whose bubble is shorter than its batch value, fix it by setting that height and re-exporting.
7. Preserve the exact source meaning. Do not invent missing text, dates, interview schedules, admissions, funding, or supervision commitments.
   - **Keep every meaningful email paragraph by default.** Greetings, thanks, interest expressions, and context sentences MUST stay in the poster (e.g. a "Thank you for your email..." opening goes into Line2 before the highlight box). Only when the text is so long it would overflow the content card may generic filler (pure courtesy phrases without information) be trimmed — never delete meaningful content to make it fit.
   - **When a long email exceeds the card capacity, fix the FIT — never let text overflow or get cut off.** The poster must always display COMPLETELY within the 1080×1440 canvas, and the bubble never grows past its fixed height. Symptom of the failure mode to avoid: the card gets stuffed with everything, grows past the canvas, and the signature mosaic ends up colliding with the bottom watermark / slogan. Remedy order (IMPORTANT — user-confirmed):
     1. **Shrink the body type size first.** Reduce every body text node in the card (DearText/Comma/Line2/HL1/HL2/Line4 — never the hero title or the school chip) from 34px down in 2px steps (32 → 30 → 28 → 26), and tighten the card's `itemSpacing` (22 → 16) plus its top/bottom padding if needed. **Do not delete any content in this step.** Re-measure the card's natural height with `capture_layout` (keep `hug_contents` while measuring) and stop as soon as it fits — then set the height back to the fixed batch value. A ~1100px card needs roughly 28px text; a ~980px card fits at 30px. Do not go below ~26px: past that the poster looks visibly different from its siblings and you must switch to step 2 instead.
     2. **Deleting content is a LAST RESORT and REQUIRES ASKING THE USER FIRST.** If even the smallest acceptable size cannot fit the text, do NOT silently cut paragraphs — tell the user the poster is over-length, show which sentence(s) you propose to drop, and wait for approval. Never trim meaningful email content on your own initiative.
     3. The poster must always display COMPLETELY — if the user does approve trimming, use this priority order:
        - Keep the decision-relevant sentences (highlight box) — these are the core.
        - Keep a SHORT version of the opening (Line2) — compress it to one sentence if needed.
        - Keep the closing/signature.
        - Compress or drop long background explanations, expanded arguments, and redundant detail — keep the gist, not the full text.
   - 邮件过长放不下时:**优先把正文字号调小**(34→32→30→28→26,同时把卡片 itemSpacing 22→16,必要时收一点上下内边距),保证全部内容都放进固定高度的卡片里、不溢出画布——这一步**不删任何内容**。只有当字号缩到可接受的最小值(约 26px)仍放不下时,才**先问用户能不能删哪一句**,得到确认后再删;严禁自己动手删有意义的段落。失败信号(必须避免):为了"全塞下"把卡片撑到超出画布,落款马赛克和底部水印/slogan 撞在一起。
8. Replace every personal or sensitive value with a subtle gray-white pixelated mosaic strip. Never use placeholder text. Cover student, professor, third-party names, email addresses, phone numbers, IDs, application numbers, account details, signatures, and other identifying data.
   - Also mosaic the student's specific research-proposal topic or exact research direction.
   - Mosaic the professor's specific research direction, named theory/model, project, grant, lab, centre, programme, dataset, or distinctive topic. Broad discipline descriptions may remain.
   - Mosaic any unusual title, affiliation detail, URL, phrase, or combination of facts that could reasonably be used to identify the specific professor.
   - When uncertain whether a detail is identifying, mosaic it.
9. Add thin red rectangular outlines around the most decision-relevant phrases without covering text.

## Output transaction (originals are KEPT)

1. Create the output folder inside the inbox using the local run date in exact `YYYY-MM-DD` format.
2. Save the finished poster there with the exact original filename and extension. Encode the image in the file's stated format; do not put PNG bytes in a `.jpg` file.
3. Verify all of the following:
   - output exists at the exact destination;
   - output opens successfully and is a portrait poster;
   - correct green, purple, or blue template was used;
   - headline and school/ranking label are legible and accurate;
   - no required personal identifier remains readable;
   - no specific RP topic, named research model/project, or professor-identifying clue remains readable;
   - red boxes do not obscure text;
   - output filename exactly matches the input filename;
   - visible source meaning is retained without fabrication;
   - **card geometry**: the white bubble bottom edge sits at the batch's fixed value (detect it by scanning upward from y=1439 for the last row where x=300/540/800 are all ≥253) and the school chip's right edge is ≤ 1008;
   - **structure**: every poster frame owns exactly 7 direct children (Hero, ContentCard, WM-A/B/C/D, Slogan). Watermarks or the slogan sitting at page level means a wrong parent id was used — move them back with `M(nodeId, frameId)`.
4. **NEVER delete or move the original screenshots.** Leave every source image exactly where it is in the inbox. Posters go only into the `YYYY-MM-DD` output folder — originals and posters coexist.
5. If generation, ranking lookup, saving, format conversion, or validation fails, leave the original untouched and report the filename and failure.
6. If an output with the same filename already exists, do not overwrite it; report the collision for review.

## Batch completion report

Report processed filenames, selected type/color, destination folder, failures retained in the inbox, and any name collisions. Do not expose the personal content that was mosaicked.
