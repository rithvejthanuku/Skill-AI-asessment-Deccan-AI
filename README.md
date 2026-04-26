# Skill-AI-asessment-Deccan-AI
Skill AI is a fully browser-based AI tool that conversationally assesses a candidate's real skill proficiency, maps gaps against a job description, and generates a personalised 90-day learning roadmap
# ✦ SkillLens — AI Skill Assessment Platform

> *A résumé tells you what they claim to know. SkillLens finds out what they actually do.*

SkillLens is a fully browser-based AI tool that conversationally assesses a candidate's real skill proficiency, maps gaps against a job description, and generates a personalised 90-day learning roadmap — all powered by Claude AI, with no backend required.

---



---

## 🌐 Live Site

**[➜ Try SkillLens Live](file:///C:/Users/thanuku/Downloads/skillagent-fixed%20(1).html)**

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
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
# Open index.html in your browser
open skillagent-fixed.html
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
Model Code:

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SkillLens — AI Skill Assessment</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Geist:wght@300;400;500;600&family=Geist+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#080810;--bg2:#0f0f1a;--bg3:#161624;--bg4:#1e1e30;--bg5:#252540;
  --border:rgba(255,255,255,0.06);--border2:rgba(255,255,255,0.1);--border3:rgba(255,255,255,0.16);
  --text:#f0f0f8;--text2:#9090b0;--text3:#55557a;
  --violet:#7c6af7;--violet2:#a78bfa;--violet3:#c4b5fd;--violet4:rgba(124,106,247,0.12);
  --teal:#2dd4bf;--amber:#f59e0b;--rose:#f87171;--green:#4ade80;--blue:#60a5fa;
  --serif:'Instrument Serif',Georgia,serif;
  --sans:'Geist',system-ui,sans-serif;
  --mono:'Geist Mono',monospace;
  --r:12px;--r2:8px;--r3:20px;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:var(--sans);font-size:15px;line-height:1.6;min-height:100vh;overflow-x:hidden}

/* ── Ambient background ── */
.ambient{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden}
.ambient-blob{position:absolute;border-radius:50%;filter:blur(100px);opacity:.18}
.a1{width:700px;height:700px;top:-200px;left:-200px;background:radial-gradient(circle,#7c6af7,transparent 70%)}
.a2{width:500px;height:500px;bottom:-100px;right:-100px;background:radial-gradient(circle,#2dd4bf,transparent 70%);opacity:.1}
.a3{width:400px;height:400px;top:50%;left:60%;background:radial-gradient(circle,#a78bfa,transparent 70%);opacity:.08}

/* ── Layout ── */
#app{position:relative;z-index:1;min-height:100vh}
.container{max-width:1080px;margin:0 auto;padding:0 32px}

/* ── Nav ── */
nav{
  position:sticky;top:0;z-index:100;
  border-bottom:1px solid var(--border);
  backdrop-filter:blur(24px);
  background:rgba(8,8,16,0.7);
}
.nav-inner{
  display:flex;align-items:center;justify-content:space-between;
  padding:16px 32px;max-width:1080px;margin:0 auto;
}
.logo{
  font-family:var(--serif);font-size:22px;font-style:italic;
  background:linear-gradient(135deg,var(--violet2),var(--teal));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  display:flex;align-items:center;gap:10px;
}
.logo-mark{
  width:28px;height:28px;border-radius:8px;
  background:linear-gradient(135deg,var(--violet),var(--teal));
  display:flex;align-items:center;justify-content:center;
  font-size:14px;-webkit-text-fill-color:white;font-style:normal;
}
.nav-right{display:flex;align-items:center;gap:12px}
.status-pill{
  display:flex;align-items:center;gap:6px;
  padding:5px 12px;border-radius:100px;
  background:var(--bg3);border:1px solid var(--border);
  font-family:var(--mono);font-size:11px;color:var(--text3);
}
.dot{width:7px;height:7px;border-radius:50%;background:var(--rose);transition:background .3s}
.dot.online{background:var(--green);box-shadow:0 0 8px var(--green)}

/* ── Pages ── */
.page{display:none}
.page.active{display:block;animation:fadeup .4s cubic-bezier(.16,1,.3,1)}
@keyframes fadeup{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}

/* ── Buttons ── */
.btn{
  display:inline-flex;align-items:center;gap:8px;
  padding:11px 22px;border-radius:var(--r2);border:none;
  font-family:var(--sans);font-size:14px;font-weight:500;
  cursor:pointer;transition:all .2s;text-decoration:none;
}
.btn-primary{
  background:var(--violet);color:#fff;
  box-shadow:0 0 0 1px rgba(124,106,247,.4),0 4px 24px rgba(124,106,247,.25);
}
.btn-primary:hover{background:var(--violet2);transform:translateY(-1px);box-shadow:0 0 0 1px rgba(167,139,250,.5),0 8px 32px rgba(124,106,247,.35)}
.btn-primary:disabled{opacity:.4;cursor:not-allowed;transform:none}
.btn-ghost{background:var(--bg3);color:var(--text);border:1px solid var(--border2)}
.btn-ghost:hover{background:var(--bg4);border-color:var(--border3)}
.btn-sm{padding:7px 14px;font-size:13px}
.btn-full{width:100%;justify-content:center;padding:14px}

/* ── Cards ── */
.card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:var(--r);padding:28px;
}
.card-sm{padding:20px}

/* ── Form elements ── */
label{display:block;font-size:11px;font-weight:500;color:var(--text3);text-transform:uppercase;letter-spacing:.8px;margin-bottom:8px;font-family:var(--mono)}
input,textarea,select{
  width:100%;background:var(--bg);border:1px solid var(--border2);
  border-radius:var(--r2);padding:11px 14px;
  color:var(--text);font-family:var(--sans);font-size:14px;
  outline:none;transition:border-color .2s,box-shadow .2s;resize:vertical;
}
input:focus,textarea:focus,select:focus{border-color:var(--violet);box-shadow:0 0 0 3px rgba(124,106,247,.12)}
input::placeholder,textarea::placeholder{color:var(--text3)}
.field{margin-bottom:18px}
.field:last-child{margin-bottom:0}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:16px}
@media(max-width:600px){.row2{grid-template-columns:1fr}}

/* ── PDF Drop zone ── */
.drop-zone{
  border:2px dashed var(--border2);border-radius:var(--r);padding:40px 24px;
  text-align:center;cursor:pointer;transition:all .25s;position:relative;
  background:var(--bg);
}
.drop-zone:hover,.drop-zone.drag-over{border-color:var(--violet);background:var(--violet4)}
.drop-zone input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.drop-icon{font-size:32px;margin-bottom:12px;display:block}
.drop-title{font-size:15px;font-weight:500;color:var(--text);margin-bottom:4px}
.drop-sub{font-size:12px;color:var(--text3)}
.drop-file-name{
  display:none;align-items:center;gap:8px;justify-content:center;
  font-family:var(--mono);font-size:13px;color:var(--violet2);margin-top:8px;
}
.drop-file-name.show{display:flex}

/* ── Hero ── */
.hero{padding:80px 0 64px}
.hero-eyebrow{
  display:inline-flex;align-items:center;gap:6px;
  padding:5px 12px;border-radius:100px;
  background:var(--violet4);border:1px solid rgba(124,106,247,.22);
  font-family:var(--mono);font-size:11px;color:var(--violet3);
  text-transform:uppercase;letter-spacing:1px;margin-bottom:24px;
}
.hero-title{
  font-family:var(--serif);
  font-size:clamp(42px,6vw,72px);
  line-height:1.02;letter-spacing:-.5px;
  margin-bottom:20px;
}
.hero-title em{font-style:italic;color:var(--violet2)}
.hero-sub{color:var(--text2);font-size:17px;line-height:1.7;max-width:560px;margin-bottom:40px}
.hero-cta{display:flex;gap:12px;flex-wrap:wrap}

.hero-grid{display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:center}
@media(max-width:768px){.hero-grid{grid-template-columns:1fr;gap:40px}}

/* Mini scorecard preview */
.preview-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:var(--r3);
  padding:24px;
}
.preview-header{
  display:flex;align-items:center;justify-content:space-between;margin-bottom:20px;
}
.preview-title{font-family:var(--mono);font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:1px}
.preview-score{font-family:var(--serif);font-size:28px;color:var(--violet2)}
.skill-row{margin-bottom:14px}
.skill-row-top{display:flex;justify-content:space-between;margin-bottom:6px}
.skill-name{font-size:13px;font-weight:500}
.skill-val{font-family:var(--mono);font-size:12px}
.bar{height:5px;background:var(--bg4);border-radius:3px;overflow:hidden}
.bar-fill{height:100%;border-radius:3px;transition:width 1.2s cubic-bezier(.16,1,.3,1)}
.g{background:linear-gradient(90deg,var(--green),#86efac)}
.t{background:linear-gradient(90deg,var(--teal),#67e8f9)}
.v{background:linear-gradient(90deg,var(--violet),var(--violet2))}
.a{background:linear-gradient(90deg,var(--amber),#fcd34d)}
.r{background:linear-gradient(90deg,var(--rose),#fca5a5)}

/* ── Section ── */
.section{padding:64px 0}
.eyebrow{font-family:var(--mono);font-size:11px;color:var(--violet3);text-transform:uppercase;letter-spacing:1px;margin-bottom:10px}
.section-title{font-family:var(--serif);font-size:34px;letter-spacing:-.3px;margin-bottom:8px}
.section-sub{color:var(--text2);font-size:15px}

/* ── Back link ── */
.back{
  display:inline-flex;align-items:center;gap:6px;
  color:var(--text3);font-size:13px;cursor:pointer;
  background:none;border:none;font-family:var(--sans);
  transition:color .2s;margin-bottom:32px;padding:0;
}
.back:hover{color:var(--text)}

/* ── Chip / badge ── */
.chip{
  display:inline-flex;align-items:center;gap:5px;
  padding:3px 10px;border-radius:100px;
  font-family:var(--mono);font-size:11px;
}
.chip-violet{background:rgba(124,106,247,.12);color:var(--violet3);border:1px solid rgba(124,106,247,.2)}
.chip-green{background:rgba(74,222,128,.1);color:var(--green);border:1px solid rgba(74,222,128,.2)}
.chip-rose{background:rgba(248,113,113,.1);color:var(--rose);border:1px solid rgba(248,113,113,.2)}
.chip-amber{background:rgba(245,158,11,.1);color:var(--amber);border:1px solid rgba(245,158,11,.2)}
.chip-teal{background:rgba(45,212,191,.1);color:var(--teal);border:1px solid rgba(45,212,191,.2)}
.chip-blue{background:rgba(96,165,250,.1);color:var(--blue);border:1px solid rgba(96,165,250,.2)}

/* ── Progress bar ── */
.progress{height:2px;background:var(--bg4);border-radius:2px;overflow:hidden;margin-bottom:32px}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--violet),var(--teal));transition:width .6s ease}

/* ── Assessment question card ── */
.q-card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:var(--r3);padding:36px;margin-bottom:20px;
  position:relative;overflow:hidden;
}
.q-card::before{content:'';position:absolute;inset:0 0 auto 0;height:2px;background:linear-gradient(90deg,var(--violet),var(--teal))}
.q-skill-row{display:flex;align-items:center;gap:10px;margin-bottom:20px;flex-wrap:wrap}
.q-num{font-family:var(--mono);font-size:11px;color:var(--text3)}
.q-text{font-family:var(--serif);font-size:22px;line-height:1.45;margin-bottom:8px}
.q-hint{font-size:13px;color:var(--text3);font-style:italic}

/* ── Answer area ── */
.answer-wrap{position:relative}
.answer-ta{
  width:100%;min-height:160px;background:var(--bg);
  border:1px solid var(--border2);border-radius:var(--r);
  padding:16px 18px;color:var(--text);font-family:var(--sans);font-size:15px;
  line-height:1.65;resize:vertical;outline:none;
  transition:border-color .2s,box-shadow .2s;
}
.answer-ta:focus{border-color:var(--violet);box-shadow:0 0 0 3px rgba(124,106,247,.1)}
.answer-footer{display:flex;align-items:center;justify-content:space-between;margin-top:10px}
.word-ct{font-family:var(--mono);font-size:11px;color:var(--text3)}

/* ── Evaluation card ── */
.eval-card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:var(--r);padding:24px;margin-bottom:20px;
  animation:fadeup .3s ease;
}
.eval-header{font-family:var(--mono);font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:1px;margin-bottom:16px}
.eval-dims{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:16px}
@media(max-width:500px){.eval-dims{grid-template-columns:repeat(2,1fr)}}
.eval-dim{text-align:center}
.eval-dim-num{font-family:var(--serif);font-size:30px;line-height:1}
.eval-dim-lbl{font-size:11px;color:var(--text3);margin-top:4px}
.eval-total{
  display:flex;align-items:center;justify-content:space-between;
  padding:12px 16px;background:var(--bg3);border-radius:var(--r2);margin-bottom:12px;
}
.eval-feedback{
  font-size:14px;color:var(--text2);line-height:1.6;
  padding:12px 16px;border-radius:var(--r2);
  border-left:3px solid var(--violet);background:var(--bg3);
}

/* ── Analysis grid ── */
.analysis-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px;margin:24px 0}

/* ── Report ── */
.report-hero{
  text-align:center;padding:48px 0 32px;
}
.score-ring{
  width:140px;height:140px;border-radius:50%;margin:0 auto 16px;
  display:flex;align-items:center;justify-content:center;
  background:conic-gradient(var(--violet) calc(var(--p,70)*3.6deg),var(--bg4) 0);
  position:relative;
}
.score-ring::after{content:'';position:absolute;inset:12px;border-radius:50%;background:var(--bg2)}
.score-inner{position:relative;z-index:1;text-align:center}
.score-num{font-family:var(--serif);font-size:38px;color:var(--violet2)}
.score-max{font-family:var(--mono);font-size:12px;color:var(--text3)}

.skill-cards{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:14px;margin:28px 0}
.sk-card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);padding:18px;transition:border-color .2s}
.sk-card:hover{border-color:var(--border2)}
.sk-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}
.sk-name{font-weight:500;font-size:14px}
.sk-score{font-family:var(--serif);font-size:22px}

/* ── Learning plan ── */
.plan-tabs{display:flex;gap:4px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--r2);padding:4px;width:fit-content;margin-bottom:24px}
.plan-tab{
  padding:7px 18px;border-radius:6px;font-size:13px;font-weight:500;
  cursor:pointer;border:none;background:none;color:var(--text2);transition:all .2s;
}
.plan-tab.active{background:var(--violet);color:#fff}
.plan-tab:hover:not(.active){background:var(--bg4);color:var(--text)}

.track-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);
  padding:24px;margin-bottom:16px;
}
.track-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:16px;flex-wrap:wrap;gap:8px}
.track-name{font-family:var(--serif);font-size:20px}
.track-meta{display:flex;gap:8px;flex-wrap:wrap;margin-top:6px}
.track-body{color:var(--text2);font-size:14px;line-height:1.65}

.resource-list{display:flex;flex-direction:column;gap:8px;margin-top:14px}
.resource-item{
  display:grid;grid-template-columns:auto 1fr auto;gap:12px;align-items:start;
  background:var(--bg3);border-radius:var(--r2);padding:12px 14px;
}
.res-icon{width:32px;height:32px;border-radius:8px;background:var(--violet4);display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
.res-title{font-size:13px;font-weight:500;margin-bottom:2px}
.res-why{font-size:12px;color:var(--text3)}
.res-hrs{font-family:var(--mono);font-size:11px;color:var(--text3);white-space:nowrap;align-self:center}

.week-list{display:flex;flex-direction:column;gap:6px;margin-top:10px}
.week-item{display:flex;gap:10px;font-size:13px;color:var(--text2);align-items:flex-start}
.week-dot{width:6px;height:6px;border-radius:50%;background:var(--violet);margin-top:6px;flex-shrink:0}

/* ── Gap / Adjacency ── */
.adjacent-item{
  background:var(--bg3);border-radius:var(--r2);padding:14px 16px;margin-bottom:10px;
  border-left:3px solid var(--teal);
}
.adj-top{display:flex;align-items:center;gap:8px;margin-bottom:4px;flex-wrap:wrap}
.adj-arrow{color:var(--teal);font-size:14px}
.adj-reason{font-size:13px;color:var(--text2)}

/* ── Loading overlay ── */
.loading{
  position:fixed;inset:0;z-index:300;
  background:rgba(8,8,16,.88);backdrop-filter:blur(12px);
  display:none;align-items:center;justify-content:center;flex-direction:column;gap:20px;
}
.loading.show{display:flex}
.spinner{
  width:48px;height:48px;border-radius:50%;
  border:3px solid var(--bg4);border-top-color:var(--violet);
  animation:spin .8s linear infinite;
}
@keyframes spin{to{transform:rotate(360deg)}}
.loading-msg{font-family:var(--mono);font-size:13px;color:var(--text2)}

/* ── Toast ── */
.toast{
  position:fixed;bottom:24px;right:24px;z-index:400;
  background:var(--bg3);border:1px solid var(--border2);border-radius:var(--r);
  padding:14px 20px;font-size:14px;max-width:320px;
  box-shadow:0 16px 48px rgba(0,0,0,.5);
  transform:translateY(80px);opacity:0;transition:all .3s cubic-bezier(.16,1,.3,1);
}
.toast.show{transform:translateY(0);opacity:1}
.toast.ok{border-color:rgba(74,222,128,.3)}
.toast.err{border-color:rgba(248,113,113,.3)}

/* ── Config modal ── */
.modal-bg{
  position:fixed;inset:0;z-index:200;
  background:rgba(8,8,16,.85);backdrop-filter:blur(10px);
  display:none;align-items:center;justify-content:center;
}
.modal-bg.show{display:flex}
.modal{
  background:var(--bg2);border:1px solid var(--border2);
  border-radius:var(--r3);padding:36px;max-width:480px;width:90%;
}
.modal h3{font-family:var(--serif);font-size:24px;margin-bottom:6px}
.modal p{color:var(--text2);font-size:14px;margin-bottom:24px}

/* ── Hiring badge ── */
.hire-badge{
  display:inline-flex;align-items:center;gap:6px;
  padding:8px 16px;border-radius:100px;font-size:13px;font-weight:500;
}
.hire-strong{background:rgba(74,222,128,.15);color:var(--green);border:1px solid rgba(74,222,128,.25)}
.hire-good{background:rgba(96,165,250,.15);color:var(--blue);border:1px solid rgba(96,165,250,.25)}
.hire-potential{background:rgba(245,158,11,.15);color:var(--amber);border:1px solid rgba(245,158,11,.25)}
.hire-poor{background:rgba(248,113,113,.15);color:var(--rose);border:1px solid rgba(248,113,113,.25)}

/* scrollbar */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--bg5);border-radius:3px}
</style>
</head>
<body>

<div class="ambient">
  <div class="ambient-blob a1"></div>
  <div class="ambient-blob a2"></div>
  <div class="ambient-blob a3"></div>
</div>

<div id="app">

<!-- ── NAV ───────────────────────────────────────────────────── -->
<nav>
  <div class="nav-inner">
    <div class="logo">
      <div class="logo-mark">✦</div>
      SkillLens
    </div>
    <div class="nav-right">
      <div class="status-pill">
        <div class="dot" id="dot"></div>
        <span id="api-lbl">Connecting…</span>
      </div>
      <button class="btn btn-ghost btn-sm" onclick="showModal()">⚙ Config</button>
    </div>
  </div>
</nav>

<!-- ── PAGE: LANDING ──────────────────────────────────────────── -->
<div id="p-land" class="page active">
  <div class="container">
    <div class="hero">
      <div class="hero-grid">
        <div>
          <div class="hero-eyebrow">✦ AI-Powered · Adaptive · Rubric-Based</div>
          <h1 class="hero-title">
            A résumé tells you<br>
            what they <em>claim</em> to know.
          </h1>
          <p class="hero-sub">
            SkillLens conversationally assesses real skill proficiency, maps gaps against the job description, and generates a personalised learning plan built around skills the candidate can <em>realistically</em> acquire.
          </p>
          <div class="hero-cta">
            <button class="btn btn-primary" onclick="show('p-create')">Start Assessment →</button>
            <button class="btn btn-ghost" onclick="showModal()">Configure API</button>
          </div>
        </div>
        <div>
          <div class="preview-card">
            <div class="preview-header">
              <div class="preview-title">Live Scorecard Preview</div>
              <div class="preview-score">7.4</div>
            </div>
            <div class="skill-row">
              <div class="skill-row-top"><span class="skill-name">Python</span><span class="skill-val" style="color:var(--green)">8.4/10</span></div>
              <div class="bar"><div class="bar-fill g" style="width:0" data-w="84%"></div></div>
            </div>
            <div class="skill-row">
              <div class="skill-row-top"><span class="skill-name">System Design</span><span class="skill-val" style="color:var(--amber)">6.1/10</span></div>
              <div class="bar"><div class="bar-fill a" style="width:0" data-w="61%"></div></div>
            </div>
            <div class="skill-row">
              <div class="skill-row-top"><span class="skill-name">PostgreSQL</span><span class="skill-val" style="color:var(--teal)">7.8/10</span></div>
              <div class="bar"><div class="bar-fill t" style="width:0" data-w="78%"></div></div>
            </div>
            <div class="skill-row">
              <div class="skill-row-top"><span class="skill-name">Kubernetes</span><span class="skill-val" style="color:var(--rose)">3.2/10</span></div>
              <div class="bar"><div class="bar-fill r" style="width:0" data-w="32%"></div></div>
            </div>
            <div style="margin-top:18px;padding-top:16px;border-top:1px solid var(--border);display:flex;gap:8px;flex-wrap:wrap">
              <span class="chip chip-violet">4 skills assessed</span>
              <span class="chip chip-teal">Adjacent: Docker → K8s</span>
              <span class="chip chip-amber">90-day plan ready</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ── PAGE: CREATE ───────────────────────────────────────────── -->
<div id="p-create" class="page">
  <div class="container section">
    <button class="back" onclick="show('p-land')">← Back</button>
    <div class="eyebrow">Step 1 of 3</div>
    <h2 class="section-title">Candidate Profile</h2>
    <p class="section-sub" style="margin-bottom:32px">Upload a PDF resume and paste the job description. AI will extract skills and identify gaps.</p>

    <div style="max-width:680px">
      <div class="card" style="margin-bottom:16px">
        <div class="row2">
          <div class="field"><label>Full Name</label><input id="f-name" type="text" placeholder="Arjun Mehta"></div>
          <div class="field"><label>Email</label><input id="f-email" type="email" placeholder="arjun@example.com"></div>
        </div>
        <div class="field" style="margin:0"><label>Company / Team (optional)</label><input id="f-company" placeholder="default" value="default"></div>
      </div>

      <div class="card" style="margin-bottom:16px">
        <label>Resume PDF</label>
        <div class="drop-zone" id="drop-zone">
          <input type="file" id="resume-file" accept=".pdf" onchange="onFileSelect(this)">
          <span class="drop-icon">📄</span>
          <div class="drop-title">Drop PDF here or click to browse</div>
          <div class="drop-sub">PDF only · Max 10 MB · Text-based (not scanned)</div>
          <div class="drop-file-name" id="file-name-display">
            <span>✓</span><span id="file-name-text"></span>
          </div>
        </div>
      </div>

      <div class="card" style="margin-bottom:20px">
        <div class="field" style="margin:0">
          <label>Job Description</label>
          <textarea id="f-jd" rows="8" placeholder="Paste the full job description here…

Example:
Senior Backend Engineer
Requirements:
- 5+ years Python (FastAPI / Django)
- PostgreSQL performance tuning, query optimisation
- Docker, Kubernetes, CI/CD pipelines
- System design for high-traffic APIs  
- AWS (ECS, RDS, S3)
- Strong communication and team leadership"></textarea>
          <div style="font-size:11px;color:var(--text3);margin-top:6px;font-family:var(--mono)">The AI extracts required skills and maps them against the resume</div>
        </div>
      </div>

      <button class="btn btn-primary btn-full" id="analyze-btn" onclick="createCandidate()">
        Analyse Skills & Continue →
      </button>
    </div>
  </div>
</div>

<!-- ── PAGE: ANALYSIS ─────────────────────────────────────────── -->
<div id="p-analysis" class="page">
  <div class="container section">
    <button class="back" onclick="show('p-create')">← Back</button>
    <div class="eyebrow">Step 2 of 3 — Skill Gap Analysis</div>
    <h2 class="section-title">Gap Report</h2>
    <p class="section-sub" style="margin-bottom:32px">Review before beginning the adaptive conversational assessment.</p>
    <div id="analysis-body" style="max-width:800px"></div>
    <button class="btn btn-primary btn-full" style="max-width:800px;margin-top:8px" onclick="startAssessment()">Begin Adaptive Assessment →</button>
  </div>
</div>

<!-- ── PAGE: ASSESSMENT ───────────────────────────────────────── -->
<div id="p-assess" class="page">
  <div class="container section" style="max-width:760px;margin:0 auto">
    <div class="progress"><div class="progress-fill" id="prog" style="width:5%"></div></div>
    <div class="q-card">
      <div class="q-skill-row">
        <span class="chip chip-violet" id="q-skill">⚡ Skill</span>
        <span class="chip" id="q-level">Intermediate</span>
        <span class="q-num" id="q-num">Question 1</span>
      </div>
      <div class="q-text" id="q-text">Loading question…</div>
      <div class="q-hint" id="q-hint"></div>
    </div>

    <div id="eval-area"></div>

    <div class="answer-wrap">
      <textarea class="answer-ta" id="answer" placeholder="Type your answer here…&#10;&#10;Be specific. Mention trade-offs, give real-world examples, explain your reasoning. The assessment is conversational — answer as you would in an interview." oninput="updateWC()"></textarea>
      <div class="answer-footer">
        <span class="word-ct" id="wc">0 words</span>
        <button class="btn btn-primary" id="sub-btn" onclick="submitAnswer()">Submit Answer →</button>
      </div>
    </div>
  </div>
</div>

<!-- ── PAGE: REPORT ───────────────────────────────────────────── -->
<div id="p-report" class="page">
  <div class="container section">
    <button class="back" onclick="show('p-land')">← New Assessment</button>
    <div id="report-body"></div>
  </div>
</div>

</div><!-- #app -->

<!-- ── LOADING ────────────────────────────────────────────────── -->
<div class="loading" id="loading">
  <div class="spinner"></div>
  <div class="loading-msg" id="loading-msg">Processing…</div>
</div>

<!-- ── TOAST ──────────────────────────────────────────────────── -->
<div class="toast" id="toast"></div>

<!-- ── CONFIG MODAL ───────────────────────────────────────────── -->
<div class="modal-bg" id="modal-bg">
  <div class="modal">
    <h3>Anthropic API Key</h3>
    <p>Get a free key at <a href="https://console.anthropic.com" target="_blank" style="color:var(--violet3)">console.anthropic.com</a> → API Keys. Free tier included.</p>
    <div class="field"><label>Anthropic API Key</label><input id="cfg-key" type="password" placeholder="sk-ant-…" autocomplete="off"></div>
    <div style="display:flex;gap:10px">
      <button class="btn btn-primary" onclick="saveConfig()">Save & Test</button>
      <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
    </div>
    <div style="margin-top:24px;padding-top:20px;border-top:1px solid var(--border)">
      <div style="font-family:var(--mono);font-size:12px;color:var(--text3);line-height:1.8">
        Model: <span style="color:var(--violet3)">claude-haiku-4-5</span> (fast &amp; affordable)<br>
        No backend required · Runs entirely in browser<br>
        PDF parsed client-side with pdf.js
      </div>
    </div>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
// ── pdf.js worker ─────────────────────────────────────────────────────────────
if(typeof pdfjsLib!=='undefined') pdfjsLib.GlobalWorkerOptions.workerSrc='https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

// ─── Anthropic API ──────────────────────────────────────────────────────────
async function gemini(prompt, retries = 2) {
  const key = S.apiKey || localStorage.getItem('anthropic_key') || '';
  if (!key) { showModal(); throw new Error('Please set your Anthropic API key first.'); }
  // Truncate prompt to save tokens
  const truncated = prompt.length > 3000 ? prompt.slice(0, 3000) + '\n[truncated for brevity]' : prompt;
  let lastErr;
  for (let attempt = 0; attempt <= retries; attempt++) {
    if (attempt > 0) await new Promise(res => setTimeout(res, 2000 * attempt));
    const r = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': key,
        'anthropic-version': '2023-06-01',
        'anthropic-dangerous-direct-browser-access': 'true'
      },
      body: JSON.stringify({
        model: 'claude-haiku-4-5-20251001',
        max_tokens: 800,
        messages: [{ role: 'user', content: truncated }]
      })
    });
    if (r.status === 429 || r.status === 529) {
      const e = await r.json().catch(() => ({}));
      const err = e.error || e;
      // Check if it's a 5-hour window rate limit
      if (err.type === 'exceeded_limit' || err.message?.includes('rate limit') || r.status === 429) {
        const resetsAt = err.resetsAt || err.resets_at;
        if (resetsAt && attempt === retries) {
          const resetTime = new Date(resetsAt * 1000).toLocaleTimeString([], {hour:'2-digit',minute:'2-digit'});
          throw new Error(`⏳ API rate limit reached. Your 5-hour usage window resets at ${resetTime}. Try again then, or use a different API key.`);
        }
        lastErr = new Error('Rate limited, retrying…');
        continue;
      }
    }
    if (!r.ok) {
      const e = await r.json().catch(() => ({}));
      lastErr = new Error(e.error?.message || ('Anthropic error ' + r.status));
      if (r.status >= 500) continue; // retry server errors
      throw lastErr;
    }
    const d = await r.json();
    let raw = (d.content?.[0]?.text || '').trim();
    if (raw.startsWith('```json')) raw = raw.slice(7);
    else if (raw.startsWith('```')) raw = raw.split('\n').slice(1).join('\n');
    if (raw.endsWith('```')) raw = raw.slice(0, raw.lastIndexOf('```'));
    return raw.trim();
  }
  throw lastErr || new Error('API call failed after retries');
}

function parseJSON(raw) {
  try { return JSON.parse(raw); }
  catch {
    // strip stray markdown
    const m = raw.match(/\{[\s\S]*\}|\[[\s\S]*\]/);
    if (m) try { return JSON.parse(m[0]); } catch {}
    return null;
  }
}

// ─── State ────────────────────────────────────────────────────────────────────
const S = {
  apiKey: localStorage.getItem('anthropic_key') || '',
  candidateId: null,
  assessmentId: null,
  questionNum: 0,
  totalQ: 0,
  currentSkill: '',
  gapData: null,
  resumeFile: null,
  // In-memory store (replaces DB)
  candidates: {},
  assessments: {},
};

// ─── Init ─────────────────────────────────────────────────────────────────────
window.addEventListener('DOMContentLoaded', () => {
  document.getElementById('cfg-key').value = S.apiKey;
  if (S.apiKey) testKey();
  else { setStatus(false); showModal(); }
  setTimeout(() => {
    document.querySelectorAll('[data-w]').forEach(el => { el.style.width = el.dataset.w; });
  }, 600);
  setupDrop();
});

// ─── Nav ──────────────────────────────────────────────────────────────────────
function show(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
}

// ─── Loading / Toast ──────────────────────────────────────────────────────────
function load(msg) { document.getElementById('loading-msg').textContent=msg; document.getElementById('loading').classList.add('show'); }
function unload() { document.getElementById('loading').classList.remove('show'); }
function toast(msg, type='') {
  const t = document.getElementById('toast');
  t.textContent=msg; t.className=`toast ${type} show`;
  setTimeout(()=>t.classList.remove('show'),3800);
}

// ─── Config ───────────────────────────────────────────────────────────────────
function showModal() { document.getElementById('modal-bg').classList.add('show'); }
function closeModal() { document.getElementById('modal-bg').classList.remove('show'); }
async function saveConfig() {
  const k = document.getElementById('cfg-key').value.trim();
  if (!k) { toast('Paste your Anthropic key first','err'); return; }
  S.apiKey = k;
  localStorage.setItem('anthropic_key', k);
  closeModal();
  await testKey();
}
async function testKey() {
  try {
    await gemini('Reply with exactly: ok');
    setStatus(true);
  } catch { setStatus(false); }
}
function setStatus(online) {
  document.getElementById('dot').className = 'dot' + (online ? ' online' : '');
  document.getElementById('api-lbl').textContent = online ? 'Anthropic Connected' : 'Set API Key ↗';
}

// ─── PDF parsing (client-side via pdf.js) ────────────────────────────────────
async function parsePDF(file) {
  const buf = await file.arrayBuffer();
  const pdf = await pdfjsLib.getDocument({data:buf}).promise;
  let text = '';
  for (let i=1; i<=pdf.numPages; i++) {
    const pg = await pdf.getPage(i);
    const tc = await pg.getTextContent();
    text += tc.items.map(it=>it.str).join(' ') + '\n';
  }
  return text.trim();
}

// ─── PDF Drop zone ────────────────────────────────────────────────────────────
function setupDrop() {
  const dz = document.getElementById('drop-zone');
  dz.addEventListener('dragover', e=>{ e.preventDefault(); dz.classList.add('drag-over'); });
  dz.addEventListener('dragleave', ()=>dz.classList.remove('drag-over'));
  dz.addEventListener('drop', e=>{
    e.preventDefault(); dz.classList.remove('drag-over');
    const f = e.dataTransfer.files[0];
    if (f) setFile(f);
  });
}
function onFileSelect(input) { if (input.files[0]) setFile(input.files[0]); }
function setFile(f) {
  if (!f.name.toLowerCase().endsWith('.pdf')) { toast('Only PDF files accepted','err'); return; }
  if (f.size > 10*1024*1024) { toast('PDF too large (max 10MB)','err'); return; }
  S.resumeFile = f;
  document.getElementById('file-name-text').textContent = f.name;
  document.getElementById('file-name-display').classList.add('show');
  document.querySelector('.drop-title').textContent = 'PDF selected ✓';
}

// ─── SKILL EXTRACTION PROMPTS (from backend/app/services/skill_extractor.py) ──
const SKILL_EXTRACT_PROMPT = `Extract skills from text. Return ONLY a JSON array, no markdown:
[{"canonical_name":"...","category":"programming_language|framework|database|cloud|devops|ml_ai|soft_skill|tool|other","proficiency_signal":"beginner|intermediate|advanced|expert|unknown","years_mentioned":null,"context":"short note"}]
Text: {text}`;

const GAP_ANALYSIS_PROMPT = `Compare candidate vs required skills. Return ONLY valid JSON, no preamble:
{"matched_skills":[{"canonical_name":"...","candidate_level":"...","required_level":"..."}],"gap_skills":[{"canonical_name":"...","required_level":"...","gap_severity":"critical|important|nice_to_have"}],"adjacent_skills":[{"gap_skill":"...","adjacent_from":"...","reason":"...","estimated_weeks_to_proficiency":2}],"bonus_skills":[{"canonical_name":"...","level":"..."}],"overall_match_percent":70,"hiring_recommendation":"strong_match|good_match|potential_match|poor_match","summary":"2 sentence summary"}
Candidate skills: {candidate_skills}
Required skills: {required_skills}`;

const LEARNING_PLAN_PROMPT = `You are a senior engineering mentor creating a personalised learning plan.
Candidate skills: {candidate_skills}
Skill gaps: {gap_skills}
Adjacent skills: {adjacent_skills}
Assessment scores: {skill_scores}
Create a 90-day roadmap. Return ONLY valid JSON:
{
  "overview": "2-3 sentence summary",
  "total_weeks": N,
  "tracks": [{"skill":"...","priority":"critical|high|medium","current_level":"...","target_level":"...","estimated_weeks":N,"leverages_existing":"...","week_by_week":["Week 1:...","Week 2:...","Week 3:..."],"resources":[{"type":"course|book|project|practice","title":"...","url_hint":"...","hours":N,"why_recommended":"..."}],"milestone":"..."}],
  "30_day_focus":["skill1"],"60_day_focus":["skill2"],"90_day_focus":["skill3"],
  "daily_hours_required":N
}`;

// ─── ASSESSMENT PROMPTS (from backend/app/agents/assessment_agent.py) ─────────
const QUESTION_GEN_PROMPT = `Generate ONE interview question. Skill:{skill} Level:{level}. Already asked:{asked}. Context:{context}. Return ONLY the question, one sentence, no preamble.`;

const RUBRIC_EVAL_PROMPT = `Score this answer. Skill:{skill} Level:{level} Q:{question} A:{answer}
Return ONLY JSON: {"correctness":0-4,"depth":0-3,"clarity":0-2,"application":0-1,"total":0-10,"justification":"one sentence","candidate_feedback":"1-2 sentences"}`;

// ─── Assessment agent logic ────────────────────────────────────────────────────
const QUESTIONS_PER_SKILL = 3;
const ADVANCE_THRESHOLD = 7;
const FALLBACK_THRESHOLD = 4;

function calcFinalSkillScore(scores) {
  if (!scores.length) return 0;
  const avg = scores.reduce((a,b)=>a+b,0)/scores.length;
  const variance = scores.length>1 ? scores.reduce((s,x)=>s+Math.pow(x-avg,2),0)/scores.length : 0;
  const consistency = Math.max(0, 1-(variance/10));
  const confidence = Math.min(1, scores.length/QUESTIONS_PER_SKILL);
  return Math.min(10, (avg*0.7)+(consistency*10*0.2)+(confidence*10*0.1));
}

// ─── Create Candidate ─────────────────────────────────────────────────────────
async function createCandidate() {
  const name    = document.getElementById('f-name').value.trim();
  const email   = document.getElementById('f-email').value.trim();
  const jd      = document.getElementById('f-jd').value.trim();
  const company = document.getElementById('f-company').value.trim() || 'default';

  if (!name || !email) { toast('Please enter name and email','err'); return; }
  if (!S.resumeFile)   { toast('Please upload a PDF resume','err'); return; }
  if (!jd)             { toast('Please paste the job description','err'); return; }
  if (!S.apiKey)    { showModal(); return; }

  load('Parsing PDF resume…');
  try {
    let resumeText = '';
    try {
      resumeText = await parsePDF(S.resumeFile);
    } catch(e) {
      throw new Error('Could not parse PDF. Make sure it\'s a text-based PDF (not a scanned image).');
    }
    if (resumeText.length < 100) throw new Error('PDF has too little text. Please use a text-based PDF.');

    load('Extracting skills from resume…');
    const resumeSkillsRaw = await gemini(SKILL_EXTRACT_PROMPT.replace('{text}', resumeText.slice(0,2500)));
    const resumeSkills = parseJSON(resumeSkillsRaw) || [];

    load('Extracting required skills from job description…');
    const jdSkillsRaw = await gemini(SKILL_EXTRACT_PROMPT.replace('{text}', jd.slice(0,2500)));
    const jdSkills = parseJSON(jdSkillsRaw) || [];

    load('Analysing skill gaps…');
    const gapRaw = await gemini(GAP_ANALYSIS_PROMPT
      .replace('{candidate_skills}', JSON.stringify(resumeSkills))
      .replace('{required_skills}', JSON.stringify(jdSkills)));
    const gap = parseJSON(gapRaw) || {matched_skills:[],gap_skills:[],adjacent_skills:[],bonus_skills:[],overall_match_percent:0,hiring_recommendation:'poor_match',summary:'Analysis failed.'};

    const candidateId = 'cand_' + Date.now();
    S.candidates[candidateId] = {
      id: candidateId, name, email, company_id: company,
      resume_text: resumeText, job_description: jd,
      extracted_skills: resumeSkills, required_skills: jdSkills,
      skill_gaps: gap.gap_skills || [],
      gap_analysis: gap, status: 'pending'
    };
    S.candidateId = candidateId;
    S.gapData = gap;

    renderAnalysis({ candidate_id: candidateId, gap_analysis: gap });
    show('p-analysis');
    toast('Skills extracted from resume ✓','ok');
  } catch(e) {
    toast(`Error: ${e.message}`,'err');
  } finally { unload(); }
}

// ─── Render Analysis ──────────────────────────────────────────────────────────
function renderAnalysis(data) {
  const gap = data.gap_analysis || {};
  const matched = gap.matched_skills || [];
  const gaps    = gap.gap_skills    || [];
  const adj     = gap.adjacent_skills || [];
  const bonus   = gap.bonus_skills  || [];
  const pct     = gap.overall_match_percent || 0;
  const rec     = gap.hiring_recommendation || '';
  const summary = gap.summary || '';

  const pctColor = pct>=70?'var(--green)':pct>=50?'var(--amber)':'var(--rose)';
  const recClass = {strong_match:'hire-strong',good_match:'hire-good',potential_match:'hire-potential',poor_match:'hire-poor'}[rec]||'hire-potential';
  const recLabel = rec.replace(/_/g,' ').replace(/\b\w/g,c=>c.toUpperCase());

  const skillTag = (s,cls) => {
    const name = typeof s==='object'?(s.canonical_name||s.skill||JSON.stringify(s)):s;
    return `<span class="chip ${cls}" style="margin:3px">${name}</span>`;
  };

  document.getElementById('analysis-body').innerHTML = `
    <div class="card" style="text-align:center;margin-bottom:16px">
      <div style="font-family:var(--mono);font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:1px;margin-bottom:16px">Match Score</div>
      <div style="font-family:var(--serif);font-size:72px;line-height:1;color:${pctColor}">${pct}%</div>
      <div style="margin-top:12px;display:flex;align-items:center;justify-content:center;gap:10px">
        <span class="hire-badge ${recClass}">${recLabel}</span>
      </div>
      ${summary?`<div style="margin-top:16px;font-size:14px;color:var(--text2);line-height:1.7;max-width:520px;margin-left:auto;margin-right:auto">${summary}</div>`:''}
    </div>
    ${gaps.length?`
    <div class="card" style="margin-bottom:16px;border-color:rgba(248,113,113,.15)">
      <div style="font-family:var(--mono);font-size:11px;color:var(--rose);text-transform:uppercase;letter-spacing:1px;margin-bottom:14px">⚠ Skill Gaps — Will Be Assessed (${gaps.length})</div>
      <div style="display:flex;flex-wrap:wrap;gap:4px">
        ${gaps.map(s=>{const name=typeof s==='object'?s.canonical_name:s;const sev=typeof s==='object'?s.gap_severity:'';const cls=sev==='critical'?'chip-rose':sev==='important'?'chip-amber':'chip-violet';return `<span class="chip ${cls}" style="margin:3px">${name}${sev?` · ${sev}`:''}</span>`;}).join('')}
      </div>
    </div>`:''}
    ${adj.length?`
    <div class="card" style="margin-bottom:16px;border-color:rgba(45,212,191,.15)">
      <div style="font-family:var(--mono);font-size:11px;color:var(--teal);text-transform:uppercase;letter-spacing:1px;margin-bottom:14px">↝ Adjacent Skills — Realistic Learning Paths</div>
      ${adj.map(a=>`
        <div class="adjacent-item">
          <div class="adj-top">
            <span class="chip chip-violet">${a.adjacent_from||'?'}</span>
            <span class="adj-arrow">→</span>
            <span class="chip chip-teal">${a.gap_skill||'?'}</span>
            ${a.estimated_weeks_to_proficiency?`<span class="chip chip-blue">~${a.estimated_weeks_to_proficiency}w</span>`:''}
          </div>
          <div class="adj-reason">${a.reason||''}</div>
        </div>`).join('')}
    </div>`:''}
    ${matched.length?`
    <div class="card" style="margin-bottom:16px;border-color:rgba(74,222,128,.15)">
      <div style="font-family:var(--mono);font-size:11px;color:var(--green);text-transform:uppercase;letter-spacing:1px;margin-bottom:14px">✓ Matched Skills (${matched.length})</div>
      <div style="display:flex;flex-wrap:wrap">${matched.map(s=>skillTag(s.canonical_name||s,'chip-green')).join('')}</div>
    </div>`:''}
    ${bonus.length?`
    <div class="card" style="margin-bottom:16px">
      <div style="font-family:var(--mono);font-size:11px;color:var(--blue);text-transform:uppercase;letter-spacing:1px;margin-bottom:14px">★ Bonus Skills (not required)</div>
      <div style="display:flex;flex-wrap:wrap">${bonus.map(s=>skillTag(s.canonical_name||s,'chip-blue')).join('')}</div>
    </div>`:''}
  `;
}

// ─── Start Assessment ─────────────────────────────────────────────────────────
async function startAssessment() {
  const cand = S.candidates[S.candidateId];
  if (!cand) { toast('Candidate not found','err'); return; }

  load('Generating first question…');
  try {
    const gap = cand.gap_analysis || {};
    const gapSkills = gap.gap_skills || [];
    const critical  = gapSkills.filter(s=>s.gap_severity==='critical').map(s=>s.canonical_name);
    const important = gapSkills.filter(s=>s.gap_severity==='important').map(s=>s.canonical_name);
    const nice      = gapSkills.filter(s=>s.gap_severity==='nice_to_have').map(s=>s.canonical_name);
    const matched   = (gap.matched_skills||[]).slice(0,2).map(s=>s.canonical_name||s);
    let skills = [...new Set([...critical,...important,...nice,...matched])].slice(0,5);
    if (!skills.length) skills = (cand.required_skills||[]).map(s=>s.canonical_name||s).slice(0,5);
    if (!skills.length) skills = ['Problem Solving','Communication','Technical Knowledge'];

    const context = `Candidate: ${cand.name}. Resume: ${(cand.resume_text||'').slice(0,400)}`;

    // Generate first question
    const firstQ = await gemini(QUESTION_GEN_PROMPT
      .replace('{skill}', skills[0])
      .replace('{level}', 'intermediate')
      .replace('{asked}', '[]')
      .replace('{context}', context));

    const assessmentId = 'assess_' + Date.now();
    const agentState = {
      candidate_id: S.candidateId,
      assessment_id: assessmentId,
      skills_queue: skills.slice(1),
      current_skill: skills[0],
      current_level: 'intermediate',
      questions_asked: [firstQ],
      answers_given: [],
      scores: [],
      evaluation_log: [],
      skill_q_count: 0,
      current_q: firstQ,
      skill_scores: {},
      is_complete: false,
      candidate_context: context,
      current_scores: [],  // scores for current skill only
    };

    S.assessments[assessmentId] = {
      id: assessmentId,
      candidate_id: S.candidateId,
      agent_state: agentState,
      status: 'in_progress',
      skill_scores: {},
      overall_score: 0,
      learning_plan: null,
    };
    S.assessmentId = assessmentId;
    S.questionNum = 1;
    S.totalQ = skills.length * QUESTIONS_PER_SKILL;

    renderQuestion({ current_skill: skills[0], current_level: 'intermediate', question: firstQ });
    show('p-assess');
    toast('Assessment started ✓','ok');
  } catch(e) {
    toast(`Error: ${e.message}`,'err');
  } finally { unload(); }
}

function renderQuestion(d) {
  const skill = d.current_skill||d.skill||'';
  const level = d.current_level||d.level||'intermediate';
  const q     = d.question||d.next_question||'';

  document.getElementById('q-skill').textContent = '⚡ '+skill;
  S.currentSkill = skill;

  const lvlEl = document.getElementById('q-level');
  lvlEl.textContent = level.charAt(0).toUpperCase()+level.slice(1);
  lvlEl.className = 'chip '+({beginner:'chip-green',intermediate:'chip-amber',advanced:'chip-rose'}[level]||'chip-amber');

  document.getElementById('q-num').textContent = `Question ${S.questionNum}`;
  document.getElementById('q-text').textContent = q;
  document.getElementById('q-hint').textContent = {
    beginner:'Tip: Define the concept clearly with a simple example.',
    intermediate:"Tip: Explain how it works and when you'd choose it over alternatives.",
    advanced:'Tip: Cover edge cases, performance implications, and system-level trade-offs.',
  }[level]||'';

  document.getElementById('answer').value='';
  document.getElementById('eval-area').innerHTML='';
  document.getElementById('sub-btn').disabled=false;
  updateWC();

  const pct = Math.max(4, Math.round(((S.questionNum-1)/Math.max(S.totalQ,1))*100));
  document.getElementById('prog').style.width = pct+'%';
}

function updateWC() {
  const w = document.getElementById('answer').value.trim().split(/\s+/).filter(Boolean).length;
  document.getElementById('wc').textContent = `${w} word${w!==1?'s':''}`;
}

// ─── Submit Answer ────────────────────────────────────────────────────────────
async function submitAnswer() {
  const ans = document.getElementById('answer').value.trim();
  if (!ans||ans.length<8) { toast('Please write a more complete answer','err'); return; }
  document.getElementById('sub-btn').disabled=true;
  load('Evaluating with AI rubric…');

  const assessment = S.assessments[S.assessmentId];
  const state = assessment.agent_state;

  try {
    // Evaluate answer
    const evalRaw = await gemini(RUBRIC_EVAL_PROMPT
      .replace('{skill}', state.current_skill)
      .replace('{level}', state.current_level)
      .replace('{question}', state.current_q)
      .replace('{answer}', ans));
    const ev = parseJSON(evalRaw) || {correctness:2,depth:1,clarity:1,application:0,total:4,justification:'Could not parse.',candidate_feedback:'Good effort!'};
    const score = parseFloat(ev.total)||0;

    // Update state
    state.answers_given.push(ans);
    state.scores.push(score);
    state.current_scores.push(score);
    state.evaluation_log.push({skill:state.current_skill,level:state.current_level,question:state.current_q,answer:ans,evaluation:ev});
    state.skill_q_count++;

    // Adapt level
    if (score>=ADVANCE_THRESHOLD && state.current_level!=='advanced')
      state.current_level = state.current_level==='beginner'?'intermediate':'advanced';
    else if (score<=FALLBACK_THRESHOLD && state.current_level!=='beginner')
      state.current_level = state.current_level==='advanced'?'intermediate':'beginner';

    unload();
    renderEval(ev, ev.candidate_feedback);

    // Check if skill is done
    if (state.skill_q_count >= QUESTIONS_PER_SKILL) {
      const finalScore = calcFinalSkillScore(state.current_scores);
      state.skill_scores[state.current_skill] = parseFloat(finalScore.toFixed(2));
      assessment.skill_scores[state.current_skill] = parseFloat(finalScore.toFixed(2));
      state.current_scores = [];
      state.skill_q_count = 0;
      state.current_level = 'intermediate';

      // Move to next skill or complete
      if (!state.skills_queue.length) {
        state.is_complete = true;
        assessment.status = 'completed';
        const scores = Object.values(state.skill_scores);
        assessment.overall_score = scores.length ? parseFloat((scores.reduce((a,b)=>a+b,0)/scores.length).toFixed(2)) : 0;

        // Generate learning plan
        load('Generating personalised learning plan…');
        const cand = S.candidates[S.candidateId];
        const gap = cand.gap_analysis||{};
        try {
          const planRaw = await gemini(LEARNING_PLAN_PROMPT
            .replace('{candidate_skills}', JSON.stringify(cand.extracted_skills||[]))
            .replace('{gap_skills}', JSON.stringify(gap.gap_skills||[]))
            .replace('{adjacent_skills}', JSON.stringify(gap.adjacent_skills||[]))
            .replace('{skill_scores}', JSON.stringify(state.skill_scores)));
          assessment.learning_plan = parseJSON(planRaw) || {overview:'Plan generation failed.',tracks:[]};
        } catch { assessment.learning_plan = {overview:'Learning plan could not be generated.',tracks:[]}; }
        unload();

        await renderReport({
          status:'completed',
          skill_scores: state.skill_scores,
          overall_score: assessment.overall_score,
          learning_plan: assessment.learning_plan,
          gap_summary: gap,
          candidate: { name: cand.name, email: cand.email },
        });
        show('p-report');
        toast('Assessment complete! 🎉','ok');
        return;
      }

      // Move to next skill
      state.current_skill = state.skills_queue.shift();
      S.questionNum++;

      setTimeout(async () => {
        load('Generating next question…');
        try {
          const nextQ = await gemini(QUESTION_GEN_PROMPT
            .replace('{skill}', state.current_skill)
            .replace('{level}', 'intermediate')
            .replace('{asked}', JSON.stringify(state.questions_asked.slice(-6)))
            .replace('{context}', state.candidate_context));
          state.current_q = nextQ;
          state.current_level = 'intermediate';
          state.questions_asked.push(nextQ);
          unload();
          renderQuestion({current_skill:state.current_skill,current_level:'intermediate',question:nextQ});
          document.getElementById('sub-btn').disabled=false;
        } catch(e) { unload(); toast(`Error: ${e.message}`,'err'); document.getElementById('sub-btn').disabled=false; }
      }, 1400);

    } else {
      // Same skill, next question
      S.questionNum++;
      setTimeout(async () => {
        load('Generating next question…');
        try {
          const nextQ = await gemini(QUESTION_GEN_PROMPT
            .replace('{skill}', state.current_skill)
            .replace('{level}', state.current_level)
            .replace('{asked}', JSON.stringify(state.questions_asked.slice(-6)))
            .replace('{context}', state.candidate_context));
          state.current_q = nextQ;
          state.questions_asked.push(nextQ);
          unload();
          renderQuestion({current_skill:state.current_skill,current_level:state.current_level,question:nextQ});
          document.getElementById('sub-btn').disabled=false;
        } catch(e) { unload(); toast(`Error: ${e.message}`,'err'); document.getElementById('sub-btn').disabled=false; }
      }, 1400);
    }

  } catch(e) {
    unload();
    toast(`Error: ${e.message}`,'err');
    document.getElementById('sub-btn').disabled=false;
  }
}

function renderEval(ev, feedback) {
  if (!ev) return;
  const total = ev.total||0;
  const color = total>=7?'var(--green)':total>=5?'var(--amber)':'var(--rose)';
  document.getElementById('eval-area').innerHTML = `
    <div class="eval-card">
      <div class="eval-header">📊 Answer Evaluated</div>
      <div class="eval-dims">
        <div class="eval-dim"><div class="eval-dim-num" style="color:var(--violet2)">${ev.correctness??'—'}<span style="font-size:14px;color:var(--text3)">/4</span></div><div class="eval-dim-lbl">Correctness</div></div>
        <div class="eval-dim"><div class="eval-dim-num" style="color:var(--teal)">${ev.depth??'—'}<span style="font-size:14px;color:var(--text3)">/3</span></div><div class="eval-dim-lbl">Depth</div></div>
        <div class="eval-dim"><div class="eval-dim-num" style="color:var(--amber)">${ev.clarity??'—'}<span style="font-size:14px;color:var(--text3)">/2</span></div><div class="eval-dim-lbl">Clarity</div></div>
        <div class="eval-dim"><div class="eval-dim-num" style="color:var(--green)">${ev.application??'—'}<span style="font-size:14px;color:var(--text3)">/1</span></div><div class="eval-dim-lbl">Application</div></div>
      </div>
      <div class="eval-total">
        <span style="font-family:var(--mono);font-size:12px;color:var(--text2)">Total Score</span>
        <span style="font-family:var(--serif);font-size:22px;color:${color}">${total} / 10</span>
      </div>
      ${(feedback||ev.candidate_feedback)?`<div class="eval-feedback">${feedback||ev.candidate_feedback}</div>`:''}
    </div>`;
}

// ─── Render Report ─────────────────────────────────────────────────────────────
async function renderReport(completionData) {
  const scores   = completionData.skill_scores||{};
  const overall  = completionData.overall_score||0;
  const plan     = completionData.learning_plan||{};
  const gap      = completionData.gap_summary||S.gapData||{};
  const cand     = completionData.candidate||{};
  const overallPct = Math.round(overall*10);
  const scoreColor = overallPct>=70?'var(--green)':overallPct>=50?'var(--amber)':'var(--rose)';

  const skillCards = Object.entries(scores).map(([sk,sc])=>{
    const p=Math.round(sc*10);
    const c=p>=70?'var(--green)':p>=50?'var(--amber)':'var(--rose)';
    const fc=p>=70?'g':p>=50?'a':'r';
    return `<div class="sk-card"><div class="sk-top"><div class="sk-name">${sk}</div><div class="sk-score" style="color:${c}">${sc.toFixed(1)}</div></div><div class="bar" style="height:5px"><div class="bar-fill ${fc}" style="width:${p}%"></div></div><div style="font-family:var(--mono);font-size:11px;color:var(--text3);margin-top:6px">${p}% proficiency</div></div>`;
  }).join('');

  const tracks = plan.tracks||[];
  function trackTab(phase) {
    const focus = plan[`${phase}_day_focus`]||[];
    const pt = focus.length ? tracks.filter(t=>focus.includes(t.skill)) : phase==='30'?tracks.filter((_,i)=>i<2):phase==='60'?tracks.filter((_,i)=>i>=2&&i<4):tracks.filter((_,i)=>i>=4);
    if (!pt.length) return `<div style="color:var(--text3);font-size:14px;padding:16px 0">No specific focus for this phase — continue with previous tracks.</div>`;
    return pt.map(t=>`
      <div class="track-card">
        <div class="track-header"><div><div class="track-name">${t.skill||''}</div><div class="track-meta">${t.priority?`<span class="chip ${t.priority==='critical'?'chip-rose':t.priority==='high'?'chip-amber':'chip-violet'}">${t.priority}</span>`:''} ${t.estimated_weeks?`<span class="chip chip-blue">~${t.estimated_weeks} weeks</span>`:''} ${t.leverages_existing?`<span class="chip chip-teal">↝ from ${t.leverages_existing}</span>`:''}</div></div></div>
        ${t.milestone?`<div style="font-size:13px;color:var(--text2);margin-bottom:12px;padding:10px 12px;background:var(--bg3);border-radius:var(--r2)">🏁 <b>Milestone:</b> ${t.milestone}</div>`:''}
        ${(t.week_by_week||[]).length?`<div class="week-list">${(t.week_by_week||[]).map(w=>`<div class="week-item"><div class="week-dot"></div><div>${w}</div></div>`).join('')}</div>`:''}
        ${(t.resources||[]).length?`<div style="margin-top:14px;font-family:var(--mono);font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">Resources</div><div class="resource-list">${(t.resources||[]).map(r=>`<div class="resource-item"><div class="res-icon">${{course:'🎓',book:'📖',project:'🛠',practice:'💪'}[r.type]||'📚'}</div><div><div class="res-title">${r.title||''}</div><div class="res-why">${r.why_recommended||''}</div></div><div class="res-hrs">${r.hours?r.hours+'h':''}</div></div>`).join('')}</div>`:''}
      </div>`).join('');
  }

  const rec=gap.hiring_recommendation||'';
  const recClass={strong_match:'hire-strong',good_match:'hire-good',potential_match:'hire-potential',poor_match:'hire-poor'}[rec]||'hire-potential';
  const recLabel=rec.replace(/_/g,' ').replace(/\b\w/g,c=>c.toUpperCase());

  document.getElementById('report-body').innerHTML = `
    <div class="report-hero">
      <div class="eyebrow">Assessment Complete</div>
      <h2 class="section-title">${cand.name||'Full Report'}</h2>
      ${cand.email?`<div style="color:var(--text3);font-size:14px;margin-bottom:20px">${cand.email}</div>`:''}
      <div class="score-ring" style="--p:${overallPct}">
        <div class="score-inner">
          <div class="score-num" style="color:${scoreColor}">${overall.toFixed(1)}</div>
          <div class="score-max">/10</div>
        </div>
      </div>
      <div style="color:var(--text2);font-size:14px">Overall Assessment Score</div>
      ${rec?`<div style="margin-top:14px"><span class="hire-badge ${recClass}">${recLabel}</span></div>`:''}
    </div>
    ${gap.summary?`<div class="card" style="margin-bottom:24px;border-color:rgba(124,106,247,.2)"><div class="eyebrow" style="margin-bottom:8px">Hiring Manager Summary</div><div style="font-size:15px;line-height:1.7;color:var(--text2)">${gap.summary}</div></div>`:''}
    <div class="eyebrow" style="margin-bottom:16px">Skill Breakdown</div>
    <div class="skill-cards">${skillCards}</div>
    ${plan.overview?`<div class="card" style="margin:28px 0 24px;border-color:rgba(45,212,191,.15)"><div class="eyebrow" style="margin-bottom:8px">Learning Plan Overview</div><div style="font-size:15px;line-height:1.7;color:var(--text2)">${plan.overview}</div><div style="margin-top:12px;display:flex;gap:8px;flex-wrap:wrap">${plan.total_weeks?`<span class="chip chip-violet">~${plan.total_weeks} weeks total</span>`:''} ${plan.daily_hours_required?`<span class="chip chip-amber">${plan.daily_hours_required}h/day</span>`:''}</div></div>`:''}
    <div class="eyebrow" style="margin-bottom:16px">Personalised 90-Day Learning Roadmap</div>
    <div class="plan-tabs">
      <button class="plan-tab active" onclick="switchTab(this,'t30')">30 Days</button>
      <button class="plan-tab" onclick="switchTab(this,'t60')">60 Days</button>
      <button class="plan-tab" onclick="switchTab(this,'t90')">90 Days</button>
    </div>
    <div id="t30">${trackTab('30')}</div>
    <div id="t60" style="display:none">${trackTab('60')}</div>
    <div id="t90" style="display:none">${trackTab('90')}</div>
    <div style="margin-top:40px;padding-top:32px;border-top:1px solid var(--border);display:flex;gap:12px;flex-wrap:wrap">
      <button class="btn btn-primary" onclick="downloadReport()">⬇ Download Report</button>
      <button class="btn btn-ghost" onclick="show('p-land')">Start New Assessment</button>
    </div>
  `;
}

function switchTab(el,id) {
  document.querySelectorAll('.plan-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  ['t30','t60','t90'].forEach(t=>document.getElementById(t).style.display=t===id?'block':'none');
}

function downloadReport() {
  const assessment = S.assessments[S.assessmentId];
  if (!assessment) return;
  const cand = S.candidates[S.candidateId]||{};
  const log = assessment.agent_state?.evaluation_log||[];
  const lines = [
    'SKILLLENS — ASSESSMENT REPORT',
    '='.repeat(50),
    `Candidate: ${cand.name||''}`,
    `Email: ${cand.email||''}`,
    `Date: ${new Date().toLocaleString()}`,
    '',
    'SKILL SCORES',
    '-'.repeat(50),
    ...Object.entries(assessment.skill_scores).map(([s,v])=>`${s.padEnd(30)} ${v.toFixed(2)}/10`),
    `${'OVERALL'.padEnd(30)} ${assessment.overall_score.toFixed(2)}/10`,
    '',
    'QUESTION LOG',
    '-'.repeat(50),
    ...log.map((l,i)=>`\n[Q${i+1}] ${l.skill} (${l.level})\nQ: ${l.question}\nA: ${l.answer}\nScore: ${l.evaluation?.total??'?'}/10  — ${l.evaluation?.justification||''}\n`)
  ];
  const blob = new Blob([lines.join('\n')],{type:'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `skilllens-report-${(cand.name||'candidate').replace(/\s+/g,'-')}.txt`;
  a.click();
}
</script>
</body>
</html>
