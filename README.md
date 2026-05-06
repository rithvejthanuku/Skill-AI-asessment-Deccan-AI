# Skill-AI-asessment-Deccan-AI
Skill AI is a fully browser-based AI tool that conversationally assesses a candidate's real skill proficiency, maps gaps against a job description, and generates a personalised 90-day learning roadmap
# ✦ SkillLens — AI Skill Assessment Platform

> *A résumé tells you what they claim to know. SkillLens finds out what they actually do.*

SkillLens is a fully browser-based AI tool that conversationally assesses a candidate's real skill proficiency, maps gaps against a job description, and generates a personalised 90-day learning roadmap — all powered by Claude AI, with no backend required.

---



---

## 🌐 Live Site

**[➜ Try SkillLens Live](https://skill-ai-asessment-deccan-ai-7l76.vercel.app/)**

> Bring your own Anthropic API key — get one free at [console.anthropic.com](https://console.anthropic.com)

---

## ✨ Features

- **📄 Resume Parser** — Drag and drop a PDF resume; AI extracts every skill with proficiency signals
- **🔍 Skill Gap Analysis** — Compares candidate skills against job description requirements; scores match percentage and flags critical gaps
- **🤖 Adaptive Assessment** — Conversational interview that adjusts difficulty (beginner → intermediate → advanced) based on live answers
- **📊 Rubric-Based Scoring** — Each answer graded on Correctness (0–4), Depth (0–3), Clarity (0–2), Application (0–1) for a total of 10
- **🗺 90-Day Learning Roadmap** — Personalised week-by-week plan with curated resources for every skill gap
- **↝ Adjacent Skill Mapping** — Shows realistic learning paths from existing skills to required ones
- **⬇ Downloadable Report** — Full assessment report exported as a `.txt` file
- **🔒 100% Client-Side** — No server, no data storage, runs entirely in your browser

---

## 🚀 How It Works

```
Upload Resume PDF  →  AI Extracts Skills  →  Paste Job Description
       ↓
  Gap Analysis  →  Adaptive Interview  →  Rubric Scoring
       ↓
  Full Report + 90-Day Learning Plan
```

### Step-by-step

1. **Configure** — Enter your Anthropic API key (saved locally in browser)
2. **Profile** — Enter candidate name, email, upload their PDF resume, paste the job description
3. **Gap Report** — Review matched skills, critical gaps, and adjacent learning paths
4. **Assessment** — Answer 3 adaptive questions per skill in a conversational interview
5. **Report** — View overall score, per-skill breakdown, hiring recommendation, and personalised learning plan

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| AI Model | Claude Haiku (claude-haiku-4-5) via Anthropic API |
| PDF Parsing | pdf.js (client-side, no upload) |
| Frontend | Vanilla HTML/CSS/JS — zero dependencies |
| Hosting | GitHub Pages / Netlify |
| Storage | localStorage (API key only) |

---

## 🖥 Running Locally

No installation required. Just:

```bash
git clone https://rithvejthanuku.github.io/Skill-AI-asessment-Deccan-AI/
cd YOUR_REPO
# Open index.html in your browser
open Skill AI Assessment.html
```

Or simply **download the HTML file** and open it in Chrome, Firefox, or Edge.

> ⚠️ Requires an [Anthropic API key](https://console.anthropic.com/api-keys). Free tier available.

---

## 🔑 API Key Setup

1. Go to [console.anthropic.com](https://console.anthropic.com/api-keys)
2. Create a new API key (starts with `sk-ant-...`)
3. Open SkillLens → click **⚙ Config** → paste your key → **Save & Test**
4. The status dot turns 🟢 green when connected

The key is stored only in your browser's localStorage and never sent anywhere except directly to Anthropic's API.

---

## 📁 Project Structure

```
skillagent-fixed.html   # Complete app — single self-contained file
README.md               # This file
```

---

## 🧠 Assessment Logic

The adaptive agent follows this flow per skill:

- Starts at **intermediate** difficulty
- If score ≥ 7 → promotes to **advanced**
- If score ≤ 4 → drops to **beginner**
- 3 questions per skill, up to 5 skills assessed
- Final skill score = weighted blend of avg score (70%) + consistency (20%) + confidence (10%)

---

## 📸 Screenshots
Final Report |
|---|---|---|
*<img width="1613" height="747" alt="image" src="https://github.com/user-attachments/assets/6fe1324e-5cd2-4e79-9568-dfa5dd267098" />
* |

---

## 🙋 FAQ

**Does this work on any computer?**
Yes — open the HTML file in any modern browser. No installation needed.

**Is my resume data stored anywhere?**
No. Everything runs in your browser. Resume text is processed in memory and never sent to any server other than Anthropic's API.

**Can multiple people use the same file?**
Yes — each person just needs to enter their own API key in ⚙ Config.

**What if I hit a rate limit?**
The app shows a friendly message with the exact reset time. Free Anthropic accounts have a 5-hour usage window.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

<div align="center">
  Built with Claude AI · Powered by Anthropic
</div>

