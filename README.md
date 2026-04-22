# // Marginalia

A single-file document review tool. Paste a PRD, spec, or any long document — read it section by section or have it read aloud — and leave comments anchored to line numbers as you go. When you're done, export a formatted summary ready to paste into Claude or any AI assistant.

No server. No build step. No dependencies. One HTML file.

## What it does

1. **Paste** your document into a line-numbered editor
2. **Choose your mode:**
   - **Read & Comment** — step through sections at your own pace
   - **Listen & Comment** — have it read aloud with natural pauses
3. **Comment** on any section — comments are tagged to exact line numbers
4. **Export** a formatted summary you can paste straight into Claude (or wherever) for revisions

## Features

- **Line-numbered editor** with live stats (lines, characters, words)
- **Markdown rendering** — headings, bold, italic, code blocks, tables, lists, blockquotes, links all render properly in the reading pane
- **Smart document chunking** — splits on paragraphs and headings, keeps tables and short sections together
- **Two review modes** — read at your own pace, or listen with auto-play
- **Auto-pause on typing** — in Listen mode, clicking into the comment box pauses playback automatically. Playback only resumes when you explicitly hit Play
- **Sentence-by-sentence TTS** — browser voices read one sentence at a time with natural pauses between them (not one long robotic stream)
- **ElevenLabs integration** — optional, for dramatically better voice quality. Paste your API key (held in memory only, never stored) and pick from your available voices. Uses the Turbo v2.5 model at 0.5 credits/character
- **Browser voice fallback** — works offline with system voices, auto-prioritises enhanced/premium voices
- **Speed and pitch controls** — tune the voice to your preference
- **Speech-to-text comments** — click the mic to dictate your comment
- **Line-anchored export** — final output references exact line numbers so your reviewer (human or AI) knows exactly where each comment applies

## Usage

Download `doc-talk.html` and open it in Chrome.

That's it.

### ElevenLabs (optional)

If you want natural-sounding voices instead of browser TTS:

1. Create a free account at [elevenlabs.io](https://elevenlabs.io)
2. Copy your API key from the dashboard
3. In Doc Talk, click **Listen & Comment**, then paste your key in the ElevenLabs tab
4. Pick a voice and hit **Start listening**

The free tier gives you 10,000 credits/month. With the Turbo v2.5 model, that's ~20,000 characters — enough for 4-5 typical PRD reviews.

> **Note:** Your API key lives in a JavaScript variable for the duration of the tab. It is never written to localStorage, cookies, or any persistent storage. Close the tab and it's gone.

> **Note:** If you're opening the file directly as `file:///...`, the ElevenLabs API calls may be blocked by CORS. Run a local server instead:
> ```
> python3 -m http.server 8080
> ```
> Then open `http://localhost:8080/doc-talk.html`.

### Export format

When you finish a review, Doc Talk generates output like this:

```
I've just reviewed the document I shared with you. Here are my comments, referenced by line number:

---
**Comment 1** — Lines 12–18
> "The platform should support real-time collaboration across..."

I think this section needs more detail on conflict resolution when two users edit simultaneously.

---
**Comment 2** — Line 45
> "Authentication will use OAuth 2.0..."

Should we also support SAML for enterprise SSO?

---

Please address each comment, referencing the line numbers, and suggest revisions where needed.
```

Paste this into Claude along with the original document and it can address each comment by line number.

## Requirements

- A modern browser (Chrome recommended for speech recognition support)
- No server, no install, no build tools

## Tech

- Vanilla HTML/CSS/JS — no frameworks, no bundler
- [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API) for browser TTS and speech-to-text
- [ElevenLabs REST API](https://elevenlabs.io/docs/api-reference) for premium TTS (optional)
- [DM Sans](https://fonts.google.com/specimen/DM+Sans) + [DM Mono](https://fonts.google.com/specimen/DM+Mono) via Google Fonts

## License

MIT
