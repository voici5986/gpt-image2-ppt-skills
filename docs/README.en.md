<div align="center">

# gpt-image2-ppt-skills

**Generate visually striking PPT decks with OpenAI `gpt-image-2` in one shot.**

A Claude Code / Codex / OpenClaw Skill. Once installed in your agent, a single natural-language prompt yields 16:9 high-res images + a ready-to-send `.pptx` — or clones any reference `.pptx` template and reskins it with new content.

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](../LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange.svg)](https://www.anthropic.com/claude-code)
[![gpt-image-2](https://img.shields.io/badge/OpenAI-gpt--image--2-black.svg)](https://platform.openai.com/docs/guides/images)

🌐 **中文** → [../README.md](../README.md)

</div>

---

## 🎬 Demo: feed one template, get a fresh deck in that style

<table>
<tr>
<th width="50%">Input: any reference template (.pptx / image)</th>
<th width="50%">Output: cloned layout + new content</th>
</tr>
<tr>
<td><img src="assets/template-demo-input.jpg" width="100%" alt="input template"></td>
<td><img src="assets/template-demo-output.jpg" width="100%" alt="generated output"></td>
</tr>
<tr>
<td align="center"><sub>English infographic template (Mass Media Infographics)</sub></td>
<td align="center"><sub>Same layout / palette / illustration vocabulary, content swapped to "how normal people make AI-powered social content"</sub></td>
</tr>
</table>

---

## ✨ What it does

- 🎨 **10 curated styles** — Spatial Glass / Tech Blue / Editorial Mono / Dark Aurora / Risograph / Wabi / Swiss Grid / Hand Sketch / Y2K Chrome / Vector Illustration, each with `cover` / `content` / `data` composition rules
- 🪄 **Template-clone mode** — drop in any `.pptx`; the agent follows its layout, palette, and illustration language, then swaps in your new content
- 🎯 **Natural-language slide edits** — say "change slide 3's subtitle", "remove the footer", or "replace these three metrics", and the agent regenerates only the target slide
- 🎮 **Dual output** — high-res PNG per slide + 16:9 `.pptx` ready to use
- ⚡ **10-way concurrency by default** — a 10-page deck finishes in ~30s
- 🧪 **Preview one slide first** — approve the cover before generating the full deck
- 🧾 **Trackable edits** — changed slides and generated versions can be traced and rolled back

## ✅ Best-fit use cases

| Use case | Fit | Notes |
| --- | --- | --- |
| Generate a new deck from a topic | Strong | Good for reports, pitches, training, courses, product intros. |
| Create a new deck from a company template | Strong | Provide a `.pptx`, approve one cover first, then run the full deck. |
| Edit titles, subtitles, dates, footers | Strong | The most stable editing scenario. |
| Update metric cards and key numbers | Good | Works, but every number must be checked before delivery. |
| Modify only one slide in a multi-slide deck | Good | The target slide is regenerated; other slides are left alone. |
| Dense tables, financial reports, legal long copy | Weak | Small text and numbers need strict human review. |

## 🧪 Editing Capability Report

If you care about "how reliable are edits in real scenes", see the user-facing case report:

- **[`docs/edit_guide.md`](./edit_guide.md)** — title replacement, date edits, footer removal, metric updates, logo insertion, single-slide edits in a multi-slide deck, current limitations, and a delivery checklist

Summary:

| Capability | Current behavior |
| --- | --- |
| Short text edits | Stable for everyday delivery. |
| Multiple explicit edits | Works best when the user clearly says what should stay unchanged. |
| Metric slides | Works, but numbers must be checked. |
| Small icon / logo insertion | Works for style-matched icons; real brand logos need source assets. |
| Native PowerPoint object editing | Not supported; output PPTX uses full-slide images. |

<details>
<summary>Developer note: internal editing mechanism diagram</summary>

<img src="assets/architecture_cn.jpg" width="100%" alt="system architecture">

</details>

## 🎨 The 10 built-in styles

> Below: the 10 styles each generating one cover under the same topic — "**How to make a PPT with gpt-image-2**". All covers are raw `gpt-image-2` output, no PS.

![10 styles · same topic, raw gpt-image-2 output](assets/style-gallery.jpg)

| Style ID | One-liner | Use cases |
| --- | --- | --- |
| `gradient-glass` | Apple Vision OS / Spatial Glass | AI product launches, technical talks, creative pitches |
| `clean-tech-blue` | Stripe / Linear-grade blue & white | Investor decks, business plans, corporate strategy |
| `vector-illustration` | Retro vector + black outlines | Education, brand storytelling, community sharing |
| `editorial-mono` | Kinfolk / Monocle editorial | Brand reveals, cultural interviews, book talks |
| `dark-aurora` | Linear / Vercel dark neon | AI products, dev tools, technical talks |
| `risograph` | Riso 2-spot-color print + halftone | Creative studios, indie zines, design agencies |
| `japanese-wabi` | Muji / Hara Kenya wabi-sabi | Tea ceremony, lifestyle, luxury, cultural lectures |
| `swiss-grid` | Bauhaus / Vignelli international grid | Academic reports, museum exhibits, serious dashboards |
| `hand-sketch` | Sketchnote / whiteboard | Workshops, product brainstorming, training |
| `y2k-chrome` | Y2K liquid chrome + butterfly stickers | Streetwear, entertainment, brand collabs, Gen-Z marketing |

---

## 🚀 Install

### Option 1: let your AI install it (recommended)

Paste this prompt into your AI assistant (Claude Code / OpenClaw / Codex / Cursor / Trae / Hermes Agent — all work) and it will handle the install:

```
Please install gpt-image2-ppt-skills for me:
https://raw.githubusercontent.com/JuneYaooo/gpt-image2-ppt-skills/main/docs/install.md
```

The agent will clone the repo, run the install script, ask for an API key only when direct API mode is needed, and tell you to restart.

### Option 2: manual install

```bash
git clone git@github.com:JuneYaooo/gpt-image2-ppt-skills.git
cd gpt-image2-ppt-skills
bash install_as_skill.sh --target claude   # Claude Code
# or
bash install_as_skill.sh --target codex    # Codex
```

The script installs the skill into the selected agent directory:

- Claude Code: `~/.claude/skills/gpt-image2-ppt-skills/`
- Codex: `~/.codex/skills/gpt-image2-ppt-skills/`

If you use direct API mode, inject environment variables through your agent
framework instead of writing secrets into the caller project's root `.env`:

- Claude Code: user-level `~/.claude/settings.json`, or project-level `.claude/settings.local.json`
- OpenClaw / custom agents: reference system env vars from `apiKey` / env config
- CI / servers: system env vars, Docker Compose, Kubernetes Secrets, or CI Secrets
- Standalone CLI: set `GPT_IMAGE2_PPT_ENV=/path/to/private.env`, or use the skill install directory `.env` as a fallback

```bash
# Variable names:
OPENAI_BASE_URL=https://api.openai.com    # or any OpenAI-compatible relay
OPENAI_API_KEY=sk-...                     # required
GPT_IMAGE_MODEL_NAME=gpt-image-2
GPT_IMAGE_QUALITY=high                    # low / medium / high / auto
```

> In **Codex**, if the current agent has native image generation, use the native path in `SKILL.md` and skip `OPENAI_API_KEY`.
>
> 🔒 **Won't accidentally eat your secrets**: the script only reads the current process env, platform-injected variables, an explicit `GPT_IMAGE2_PPT_ENV`, and the skill install directory `.env` fallback. It does **not** walk up into caller project directories.
>
> 🪄 Template-clone mode additionally needs native `libreoffice` (to render `.pptx` → PNG).

---

## 🛠 How to use inside Claude Code

Once installed, just say it in plain English:

> Use **gpt-image2-ppt** to make a 5-slide deck about **[your topic]**, style = `dark-aurora`.

Template clone, same shape:

> I have a `company-template.pptx` — make a 5-slide deck about **[your topic]** using that template.

Claude will write the `slides_plan`, generate a cover first for you to approve, then run the full deck and hand back the `.pptx` path.

> Prefer to call the CLI yourself instead of going through an agent? See [`SKILL.md`](../SKILL.md) — CLI flags and file layout live there.

---

## 📚 More Docs

- **[`docs/edit_guide.md`](./edit_guide.md)** — user-facing editing capability report, cases, summary, limitations, and delivery checklist
- **[`docs/workflow.md`](./workflow.md)** — developer documentation for CLI dispatch, generation / edit / rollback / ingest flows, version history, and data safety
- **[`SKILL.md`](../SKILL.md)** — agent execution spec for generation, template clone, Codex native path, editing workflow, and command references

---

## 🙏 Acknowledgements

- [op7418/NanoBanana-PPT-Skills](https://github.com/op7418/NanoBanana-PPT-Skills) — reference for the original style prompts and early skill structure. This project swaps the image backend from Nano Banana Pro to OpenAI gpt-image-2, rewrites the 3 inherited styles and adds 7 new ones (10 total), and layers on template-clone mode (vision-based style extraction from any user `.pptx`), an md-first authoring flow, automatic `.pptx` packaging, and a codex CLI fallback backend.
- [lewislulu/html-ppt-skill](https://github.com/lewislulu/html-ppt-skill) — reference for the Claude Code skill `SKILL.md` frontmatter.

## License

Apache License 2.0 — see [LICENSE](../LICENSE).
