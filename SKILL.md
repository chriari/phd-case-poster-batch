---
name: phd-case-poster-batch
description: Manually batch-process PhD outreach email, interview invitation, and offer screenshots into 乐意轻学 branded posters. Use only when the user explicitly asks to process images from a user-specified folder (or a named test subfolder), classify screenshots as 套磁回复/面试邀请/Offer, select the green/purple/blue template, verify current university rankings, mosaic personal data, preserve each input filename exactly, archive finished posters in a YYYY-MM-DD folder, and remove originals only after successful validation. Do not schedule or monitor automatically.
---

# 博士案例海报批处理

Read [references/template-rules.md](references/template-rules.md) completely before processing images.

## Usage briefing (MUST tell the user before every run)

Before doing anything, briefly explain to the user how this run will work, in plain language:

1. **Input folder**: ask the user which folder holds the screenshots (or confirm the folder from the previous run).
2. **Output**: posters are saved inside that folder under a `YYYY-MM-DD` subfolder (today's date), keeping the original filenames exactly.
3. **Flow**: each screenshot is read and classified (普通回复 → green / 面试邀请 → purple / Offer → blue), the latest QS/USNEWS ranking is verified online, then each poster is built on the Ardot canvas with the approved style and exported as PNG.
4. **Privacy**: all personal/sensitive info (names, emails, signatures, research topics) is covered with gray mosaic blocks; key sentences are outlined in red. Nothing sensitive is ever shown in the report.
5. **Original files**: after a poster passes validation, the original screenshot is moved to the Trash (recoverable). If anything fails, the original is left untouched.
6. **First-time tip**: for a brand-new environment/colleague, recommend running 1-2 test images first to confirm font rendering before batch processing.

## Fixed locations

- Inbox: the **user-specified input folder**. Ask the user for the folder path at the start of each run (or reuse the folder from the previous run if unchanged). Never hard-code any specific user's desktop path — this skill may be shared with other colleagues.
- Run only after the user explicitly asks. Never create a timer, recurring automation, watcher, or background monitor for this workflow.
- Treat supported image files placed directly in the inbox as unprocessed inputs.
- If the user explicitly names or approves a test subfolder, treat supported image files directly inside that one subfolder as the current batch inputs.
- Otherwise ignore `.DS_Store`, hidden files, and all subfolders; dated subfolders are outputs, not inputs.
- Style source: follow the design spec in [references/template-rules.md](references/template-rules.md) (2026-08 年轻互联网版). The old images in `assets/` are deprecated and NOT to be used as style references.
- Known Ardot pitfall (IMPORTANT for stable reproduction): creating poster frames by Copying a sample frame can render with stale/wrong content (screenshots/exports show other posters' Hero text) even though node data is correct — observed when two frames' contents appeared swapped. **Stable, reproducible workflow:**
  1. Create a FRESH Ardot design file for each batch (never reuse a file that has shown rendering issues).
  2. Build every poster from scratch with Insert (I) operations only — do NOT Copy the sample frame. Use the exact parameter tables in `references/template-rules.md`.
  3. Build all frames before exporting; verify content by reading node data, then export PNG at scale=1 and do a pixel-diff sanity check against a known-good reference (same-content frames should differ <5%, different-content frames should differ >8%).
  4. If a file starts rendering mixed content, abandon it and start a new file.

## Process each input

1. Record the exact filename, including capitalization, punctuation, spaces, Chinese characters, and extension. Never rename it.
2. Inspect and transcribe only visible screenshot content. Use the filename only as a hint and output identifier.
3. Resolve conflicts in favor of the screenshot: school, country/region, content type, and facts visible in the screenshot override the filename and user-supplied labels.
4. Classify before choosing a template:
   - formal admission or conditional/unconditional offer → blue Offer;
   - explicit interview, meeting, Zoom, Teams, or further-conversation invitation → purple interview;
   - ordinary reply, material request, process guidance, research/funding discussion, or supervision possibility without a meeting invitation → green outreach reply.
   - When multiple classes are explicit, use Offer > interview > ordinary reply.
5. Identify the school from screenshot evidence. Verify the latest public ranking immediately before generation:
   - United States: latest U.S. News Best Global Universities rank; label `学校中文名｜USNEWS数字`.
   - Other countries/regions: latest QS World University Rankings; label `学校中文名｜QS数字`.
   - Show the ranking only when the numeric rank is 200 or better. If the rank is greater than 200, or the entire published ranking band begins after 200, show only the Chinese school name.
   - Do not include ranking year, “世界大学排名”, or “第”.
   - For Sino-foreign joint-venture universities, use `中外合办-PHD` as the title region; do not use `中国-PHD`.
6. Generate a branded poster on the Ardot canvas following the layout, color, type, watermark, and mosaic rules in [references/template-rules.md](references/template-rules.md). Use the type/color mapping (green/purple/blue) from the classification. Then export the poster frame as PNG.
7. Preserve the exact source meaning. Do not invent missing text, dates, interview schedules, admissions, funding, or supervision commitments.
8. Replace every personal or sensitive value with a subtle gray-white pixelated mosaic strip. Never use placeholder text. Cover student, professor, third-party names, email addresses, phone numbers, IDs, application numbers, account details, signatures, and other identifying data.
   - Also mosaic the student's specific research-proposal topic or exact research direction.
   - Mosaic the professor's specific research direction, named theory/model, project, grant, lab, centre, programme, dataset, or distinctive topic. Broad discipline descriptions may remain.
   - Mosaic any unusual title, affiliation detail, URL, phrase, or combination of facts that could reasonably be used to identify the specific professor.
   - When uncertain whether a detail is identifying, mosaic it.
9. Add thin red rectangular outlines around the most decision-relevant phrases without covering text.

## Output and deletion transaction

1. Create the output folder inside the inbox using the local run date in exact `YYYY-MM-DD` format.
2. Save the finished poster there with the exact original filename and extension. Encode the image in the file's stated format; do not put PNG bytes in a `.jpg` file.
3. Before deleting the input, verify all of the following:
   - output exists at the exact destination;
   - output opens successfully and is a portrait poster;
   - correct green, purple, or blue template was used;
   - headline and school/ranking label are legible and accurate;
   - no required personal identifier remains readable;
   - no specific RP topic, named research model/project, or professor-identifying clue remains readable;
   - red boxes do not obscure text;
   - output filename exactly matches the input filename;
   - visible source meaning is retained without fabrication.
4. Delete the original input only after every check passes. Deletion is explicitly authorized only for successfully processed source images in the inbox root or in the one test subfolder explicitly approved for the current run.
5. If generation, ranking lookup, saving, format conversion, or validation fails, leave the original untouched and report the filename and failure. Never delete on partial success.
6. If an output with the same filename already exists, do not overwrite it and do not delete the input; report the collision for review.

## Batch completion report

Report processed filenames, selected type/color, destination folder, failures retained in the inbox, and any name collisions. Do not expose the personal content that was mosaicked.
