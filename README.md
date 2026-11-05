# Wrongly — Variety + Better Voice edition

A 3-round game (5 questions per round) featuring Classic (4-second typing), Speech-to-Text (4-second speaking), and Wrongly Blitz (1.5-second speaking).

## Updates
- Nearly 200 hand-written prompts spanning 19 categories, from sports, jobs, weather and music to everyday objects; no number-sequence, calendar-month, or space questions.
- Each game draws 15 fresh prompts with a different category for each question when possible, reducing repetitive topics.
- In voice modes, recording lasts for the answer window **plus a 650 ms audio tail** to avoid clipping word endings. The timer still ends at 1.5 s in Blitz or 4 s in Speech-to-Text. Audio is sent to the AI **after** recording ends. There may be a short delay before the next question.
- Voice transcription is not the same as AI grading: transcription uses the OpenAI API; answer checking uses curated category vocabulary plus typo correction.

## Publish updates to your already-live Render website
1. Open your GitHub `wrongly` repository.
2. Upload/replace these files at repository root: `index.html`, `server.js`, `package.json`, `README.md`.
3. Commit the changes. Render will usually redeploy automatically; otherwise choose Manual Deploy > Deploy latest commit.
4. Refresh your Render URL (on Chrome press Ctrl+Shift+R).
5. Test **Classic** first, then select **Wrongly Blitz** and allow microphone access.

## Voice configuration
Render > Wrongly > Environment must contain `OPENAI_API_KEY` with a valid key for transcription. **Never include this key in GitHub or the HTML**. API use can cost money.

`GET /api/status` reports whether transcription is configured. If voice returns no text despite audible speaking, check Render logs for transcription errors, mic permissions, audio input selection, and the AI account's API billing. The browser's microphone permission alone does not guarantee successful AI transcription.

### Notes
- The 650 ms tail helps catch the last sound of an answer that **began before the timer ended**. It is not a fully tamper-proof speech-onset validator. A later production version should use voice-activity detection and timestamped audio to prevent words started after the buzzer from counting.
- Hosted HTTPS is required for microphone recording on Chrome. Opening an HTML file directly from Downloads may not work.
- No global accounts or online leaderboards yet. The current score is stored in the player's browser.


V3: Classic mode saves whatever is typed when the 4-second timer ends, even without Enter. Read-aloud is optional and starts the timer AFTER reading. Speed options: 1.0x, 1.5x, 2.0x, 2.5x. AI fallback grading for unexpected plausible answers uses /api/grade and the server OPENAI_API_KEY; when unavailable, the built-in word list is used. AI grading can incur API charges.
