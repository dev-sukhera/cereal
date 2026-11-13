# CerealBox AI Studio

This project is a local prototype for the CerealBox Agency AI automation challenge. Its custom Flask, HTML, CSS and JavaScript interface runs on your computer; nothing is deployed.

## What this project does

Each of the nine challenge workflows has its own section, arranged in a guided sequence:

1. **AI Idea Generator:** generate five distinct concepts with an audience insight, strategic rationale, core message, execution, test hypothesis, goal-aligned KPI and evidence to verify. One is labeled as an objective-based recommended starting point, not a performance prediction.
2. **AI Copywriting:** select an idea and generate hooks, headlines and primary text. Choose a primary-text variant to carry into the landing-page preview and download.
3. **AI Landing Pages:** preview and download a responsive, standalone HTML page with the offer details and selected ad-copy variant carried through. The product-style artwork is illustrative, not a generated product image.
4. **AI Static Creative:** build an editable image prompt from the brief, selected idea, visual direction and aspect ratio. Copy it to an external image model; this app does not render images.
5. **AI Script Writing:** generate a continuous 15-, 30-, 45- or 60-second script, then regenerate with a runtime improvement request. OpenAI mode applies the request; local-template mode attaches it as a clearly labeled production note.
6. **AI UGC Video:** build a copyable creator-style video prompt and shot outline with claim-safety guidance. It does not generate video.
7. **AI Video Editing:** require a source video, read its duration, and sample three frames in the browser. When an OpenAI key is configured, send only those still frames, their timestamps, the duration, optional script context, and editing notes to the model for three visual edit recommendations and a video-aware continuous cut plan. Preview cuts locally and split clips at their midpoint. The original video is never uploaded; rendered/exported edits are not included.
8. **AI Media Buyer / Ads Agent:** get a rule-based launch plan, daily budget allocation, success metrics and guardrails from the campaign brief. This planning section is separate from results reporting and cannot control ad accounts.
9. **Toast / Meta Ads Analysis:** view sample CSV metrics, recommendations, a ROAS bar chart and a conversion-share chart.

No live advertising accounts are connected. The Meta demo reveals the bundled CSV; it does not authenticate or retrieve live data. The landing-page export is a single HTML file with embedded CSS; review its placeholder button links, product details and claims before publishing. Approved campaign snapshots are saved in this browser's local storage and can be reopened from **Approved drafts** in the sidebar or top bar. Choose **Edit draft** to reopen one in the studio; regenerate the campaign after changing its brief, then **Save changes & approve** to replace the archived version. After approval, choose **Start new campaign** to return to the brief form; the approved snapshot stays archived. Drafts are not uploaded or published. OpenAI use requires an API key and internet access, and may incur charges. For video edit analysis, only three sampled still frames and video metadata are sent to OpenAI; do not use footage you are not allowed to share with the configured provider.

## Project structure

```text
cerealbox-ai-studio/
├── README.md
├── pyproject.toml
├── uv.lock
├── .env.example
├── .gitignore
├── samples/
│   └── video-editing-sample.mp4
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── data/
│   │   ├── mock_ads.csv
│   │   └── sample_campaigns.json
│   ├── modules/
│   │   ├── __init__.py
│   │   ├── analytics.py
│   │   ├── editing.py
│   │   ├── generators.py
│   │   ├── idea_recommendation.py
│   │   ├── image_prompt.py
│   │   ├── landing_export.py
│   │   ├── llm_service.py
│   │   ├── media_buyer.py
│   │   └── ugc_prompt.py
│   ├── static/
│   │   ├── app.js
│   │   └── styles.css
│   ├── templates/
│   │   └── index.html
│   └── utils/
│       ├── __init__.py
│       └── prompts.py
├── docs/
│   ├── PROJECT_EXPLANATION.md
│   ├── WORKFLOW_MAP.md
│   └── ROADMAP.md
└── tests/
    ├── test_generators.py
    └── test_web_app.py
```

## Quick start with uv

This project uses `uv` for dependency management.

1. Install uv if needed:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. Create and sync the local environment:

```bash
cd cerealbox-ai-studio
uv venv
uv sync
```

3. Configure the OpenAI API key locally if you do not already have `.env`:

```bash
test -f .env || cp .env.example .env
```

If you created `.env` already, keep it; do not overwrite it. Otherwise, edit `.env` and replace the example value with your key. `.env` is ignored by git and must not be shared or committed. The app can run without a key using local demo templates. If an OpenAI request fails (for example, because a key is invalid or unavailable), the campaign ideas, selected-idea ad copy, video script or edit timeline falls back to local demo output rather than interrupting the demo; the source label identifies the fallback. Successful OpenAI requests may incur API charges.

4. Start the app locally:

```bash
uv run python -m app.main
```

5. Open `http://127.0.0.1:5000` in your browser. The server binds to your computer only. Keep the terminal open while using the app and press Ctrl+C to stop it.

## Demo flow

The app is a local, end-to-end workflow prototype:

1. Enter a campaign brief and generate campaign concepts.
2. Select an idea and use the workflow navigation to continue to ad copy. Review the hooks, headlines and body-copy variants; the selected primary text carries into the next page.
3. Review the landing-page preview and download its standalone HTML draft.
4. Continue in order through **AI Static Creative**, **AI Script Writing**, **AI UGC Video**, **AI Video Editing**, and **AI Media Buyer**. Each page has previous/next controls; direct tabs remain available too.
   In **AI Video Editing**, choose a video (up to 100 MB and 3 minutes). Generating a plan extracts three sampled stills locally and sends those images and the video duration to the configured AI. The full video remains in your browser. A five-second sample is available at [`samples/video-editing-sample.mp4`](./samples/video-editing-sample.mp4).
5. In **Toast / Meta Analysis**, click **Connect to Meta (demo)** to reveal the sample report and charts; all displayed data comes from the included CSV.
6. Use **Approve draft** to open the completion review for the eight required campaign-building steps. Each step is listed as complete or incomplete, with a shortcut to unfinished work; confirm approval once all required steps are complete. Human review and Toast / Meta Ads Analysis are optional. Find approved snapshots from **Approved drafts** in the sidebar or top bar; use **Edit draft** to reopen a snapshot and **Save changes & approve** to replace its archived version. After approval, **Start new campaign** returns to the brief form while keeping the snapshot in the archive. They remain in this browser only and are not published.

The left navigation sidebar can be expanded on desktop and tablet with its chevron control. The workspace shifts over to preserve the layout rather than being covered; on narrow phones it stays compact to keep room for the page.

## Challenge coverage

This app covers the required CerealBox challenge areas in a practical, mock environment:

- AI Copywriting
- AI Static Creative
- AI Script Writing
- AI UGC Video
- AI Video Editing (video-duration and three-frame AI analysis; original video stays local; no rendered export)
- AI Media Buyer / Ads Agent
- AI Idea Generator
- AI Landing Pages
- Toast / Meta Ads Analysis

## Quality controls included

- brand input and constraints
- human approval checklist
- policy-safe guidance inside the brief
- mock performance dashboard to guide recommendation logic

## Notes

This is a prototype to show thinking, workflow design and practical implementation. It is not a full production-ready agency platform, but it is structured in a way that can be extended into a real AI automation system over time. Running the local app sends campaign-generation prompts to OpenAI when a valid API key is configured; do not enter confidential client information into this demo.

## Where each area stands (and how to take it further)

Quick honest breakdown. Some areas are wired to a real model and work end to end. Others are a clear workflow with mock logic in the middle, so you can see the shape before we plug real tools in.

**Built in depth** (real OpenAI calls, with a local fallback): Idea Generator, Copywriting, Script Writing, Video Editing analysis.
**Built at workflow level** (UI and flow are real, the "engine" is a prompt, template or rule set): Static Creative, UGC Video, Landing Pages, Media Buyer, Toast / Meta Analysis.

### AI Idea Generator
- **Done:** five structured concepts from the brief (insight, rationale, message, KPI, test hypothesis), with one marked as the recommended starting point. It feeds every step after it.
- **Next:** give it memory. Store past campaigns and their real results, then pull the best and worst performers into the prompt (simple RAG over Postgres or pgvector). Add a second "critic" pass that scores ideas for novelty and brand fit before a strategist sees them.

### AI Copywriting
- **Done:** hooks, headlines and primary text generated from the selected idea. The chosen variant flows into the landing page.
- **Next:** a per-client brand voice file plus a small "approved copy" library as examples. Add automatic checks for character limits, banned words and Meta policy-sensitive claims. Push approved variants straight into ad drafts.

### AI Script Writing
- **Done:** timed 15/30/45/60-second scripts, plus regeneration from a feedback note.
- **Next:** script templates per format (UGC, testimonial, explainer), and a hook library scored against past thumb-stop rates from Toast data.

### AI Video Editing
- **Done:** reads the video's duration, samples three frames in the browser, and sends only the stills to the model to get edit suggestions and a cut plan. You can preview and split clips locally.
- **Abstract:** no real render or export yet.
- **Next:** turn the cut plan into an actual render.
  - **FFmpeg** (free) for cuts, trims and burned-in captions.
  - **Shotstack** or **Creatomate** if we want a hosted, template-based render API.
  - **Whisper** or **Deepgram** for transcripts and captions.
  - **ElevenLabs** for voiceover.
  - Royalty-free B-roll from the **Pexels** or **Storyblocks** APIs.
  - An editor still signs off on the final cut.

### AI Static Creative
- **Abstract:** builds a solid image prompt from the brief, idea, direction and aspect ratio, but doesn't render anything.
- **Next:**
  - **OpenAI gpt-image-1** for general concepts.
  - **Ideogram** when text on the image matters.
  - **Flux**, via Replicate or fal.ai, for style control.
  - The real win is compositing: generate the background or scene with AI, then drop in the real product shot, logo and copy using **Bannerbear**, **Placid** or our own HTML-to-image templates. That keeps brand assets pixel-perfect and avoids AI-mangled logos.

### AI UGC Video
- **Abstract:** produces a creator-style prompt and shot list with claim-safety notes. No video is generated.
- **Next:** the APIs that handle UGC-style output best right now:
  - **HeyGen**: solid avatar API, good lip-sync, multilingual.
  - **Arcads** and **Creatify**: built specifically for UGC-style ads, and fast for testing many hooks.
  - **Captions (Mirage)**: very natural-looking "talking to camera" output.
  - **ElevenLabs** if we want our own voice track on top.
  - My take: use AI avatars for hook testing and volume. Keep real creators for hero ads and anything with a testimonial, since disclosure and trust matter here, especially for fundraising clients.

### AI Landing Pages
- **Abstract:** a standalone HTML page built from a template, filled with the offer and selected copy.
- **Next:** have the model output structured sections (hero, proof, FAQ, CTA) as JSON. Render them through a small component library, then publish via the **Webflow CMS API** or a **Next.js on Vercel** setup. Add A/B variants and track conversions back into Toast. A designer reviews before anything goes live.

### AI Media Buyer / Ads Agent
- **Abstract:** a rule-based launch plan, budget split and guardrails. It can't touch any ad account.
- **Next:** start read-only. The agent watches Toast data and posts alerts and recommendations to **Slack**, for things like CPA spikes, creative fatigue or budget pacing. Once trust is there, it can take small pre-approved actions (pause an ad, shift a capped budget) through the Meta Marketing API, each one needing a one-click human approval and written to an audit log. Never fully autonomous on spend.

### Toast / Meta Ads Analysis
- **Abstract:** reads a mock CSV and shows metrics, recommendations and charts.
- **Next:** see the plan below.

### Meta Ads integration: the small, human plan
1. **Days 1–5:** set up a Meta developer app under CerealBox's Business Manager. Create a system user with **read-only** (`ads_read`) access to a test ad account first, then client accounts once they approve.
2. **Days 6–10:** a nightly job pulls the Marketing API **Insights** endpoint (spend, clicks, conversions, CTR, CPC, ROAS, plus impressions and date) into Postgres. It's mostly the same columns as the current CSV, so the dashboard needs only small changes.
3. **Days 11–30:** Toast switches from the CSV to the database. Add cross-client rollups and a short AI-written summary each morning ("what changed and why it matters"), sent to Slack.
4. **Days 60–90:** only after the team trusts the numbers, request `ads_management` for approved actions through the Media Buyer agent. Keep tokens in a secrets manager, respect API rate limits, and log every call.

Nothing here touches live accounts until the client and the team say yes.

### Timeline (2 weeks → 90 days)

The order is simple. Start where data and text already work and the risk is low, then move to the expensive media work. Anything that can spend money comes last.

| When | What we tackle | Why this first | Deliverable | Done when |
|---|---|---|---|---|
| **First 2 weeks** | Idea Generator, Copywriting, Meta read-only access | Cheap, fast to test, and every other area depends on ideas, copy and real data | Brand voice files for 2–3 clients, campaign history store, Meta test account connected | Strategists approve 3 out of 5 ideas without heavy edits; Insights data lands in the database every night |
| **30 days** | Script Writing, Toast on live data, Static Creative | Scripts reuse the copy setup; Toast gives everyone a reason to open the tool daily | Toast dashboard on real data with a morning Slack summary; first rendered static ads using brand templates | Toast numbers match Ads Manager within 2%; designers use at least half the generated statics as a starting point |
| **60 days** | Landing Pages, Video Editing render, UGC Video pilot | Needs the copy and creative pieces above to be stable first | Landing pages published from JSON sections; FFmpeg/Shotstack renders with captions; 10 AI UGC hook tests | A page goes from brief to live in under a day; edited videos need only light touch-ups; UGC tests reach normal CTR benchmarks |
| **90 days** | Media Buyer agent, closing the loop | Needs trusted data and a good track record from Toast first | Slack alerts + one-click approved actions with an audit log; ad results fed back into the Idea Generator | No unapproved spend changes; alerts are useful (most get acted on, few false alarms); measurable hours saved per campaign |

**Main dependencies:** client approval for Meta access, a few hours of time from a strategist and a designer each week for review, and an API budget (roughly a few hundred dollars a month at pilot scale, mostly for video).

### What I'd build next if I joined
1. Toast on live data first. It's the quickest visible win, and it feeds everything else.
2. A shared brand and campaign memory, so ideas and copy get better with every campaign instead of starting from zero.
3. A proper review queue (approve, edit, reject with a reason) and logged feedback, so we can measure quality instead of guessing.
4. Then grow the media side (statics, video, UGC) one client at a time.

The detailed version lives in [docs/ROADMAP.md](./docs/ROADMAP.md).
