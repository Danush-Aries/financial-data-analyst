<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:0d47a1,50:00ffff,100:00ff41&text=Financial%20Data%20Analyst&fontSize=42&fontColor=ffffff&animation=fadeIn&desc=Claude%20%C2%B7%20Next.js%2014%20%C2%B7%20CSV%20%2F%20PDF%20%C2%B7%20Charts&descAlignY=80&descSize=16" width="100%" alt="banner"/>
</div>

<div align="center">

![Next.js](https://img.shields.io/badge/Next.js_14-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Anthropic](https://img.shields.io/badge/Claude_API-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![Recharts](https://img.shields.io/badge/Recharts-22B5BF?style=for-the-badge)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-00ff41?style=for-the-badge)

</div>

Drop a **CSV** or **PDF** of your financial data and chat with it. The app sends parsed data + your question to **Claude**, which returns plain-English analysis **and** a JSON chart spec — automatically rendered with **Recharts** in the conversation. Line, bar, pie, area, scatter, radar — Claude picks the right visualization for the question.

## 🏗️ How it works

```mermaid
flowchart LR
    F[📁 CSV / PDF upload] -->|papaparse / pdf-parse| P[Parsed data]
    Q[💬 User question] --> API[POST /api/chat]
    P --> API
    API -->|system prompt + data| C[Claude API]
    C -->|markdown + ```chart{...}```| EX[Chart extractor]
    EX -->|JSON spec| CR[Recharts renderer]
    EX -->|cleaned text| MSG[Message bubble]
    CR --> UI[Chat UI]
    MSG --> UI
```

## ✨ Features

- 📊 **Auto-generated charts** — Claude embeds a fenced `chart` block when a visualization helps; the UI renders it inline
- 📁 **CSV + PDF ingestion** — `papaparse` for CSV, `pdf-parse` for PDFs; first ~20 rows previewed in a data table
- 📈 **6 chart types** — line, bar, pie, area, scatter, radar — Claude picks based on the question
- 🎯 **KPI-focused analysis** — trends, anomalies, percentages, specific numbers (no fluff)
- 🎨 **Polished Next.js UI** — Tailwind + Radix dialogs / tabs / toast, lucide icons, dark-mode CSS vars
- 💾 **Export chart as image** — `html-to-image` snapshot of any rendered chart

## 🚀 Quick start

```bash
git clone https://github.com/Dhanush-Aries/financial-data-analyst.git
cd financial-data-analyst
npm install

cp .env.example .env.local            # then add ANTHROPIC_API_KEY
npm run dev                           # http://localhost:3000
```

## 🛠️ Tech stack

**Next.js 14** (App Router) · **@anthropic-ai/sdk** · **Recharts** · **Tailwind CSS** + Radix UI · **TypeScript** · **papaparse** + **pdf-parse**

## ⚙️ Environment

| Variable | Required | Description |
|---|---|---|
| `ANTHROPIC_API_KEY` | ✅ | Get it at [console.anthropic.com](https://console.anthropic.com) |

## 📂 Project structure

```
├── app/
│   ├── api/chat/route.ts   # Claude API route with financial system prompt
│   ├── page.tsx            # Main chat UI + file upload + data preview
│   ├── layout.tsx          # Root layout
│   └── globals.css         # Tailwind base + CSS variables
├── components/
│   ├── FileUpload.tsx      # Drag-drop CSV / PDF
│   ├── DataTable.tsx       # Preview parsed rows
│   └── ChartRenderer.tsx   # Recharts dispatcher (line / bar / pie / area / scatter / radar)
└── lib/
    └── fileParser.ts       # CSV (papaparse) + PDF (pdf-parse) parsers
```

## 💡 Example prompts

- *"What were the top 3 revenue months last year and how did they trend?"*
- *"Compare expenses across categories — which one grew fastest?"*
- *"Plot revenue vs cost per quarter."*
- *"Find any anomalies in this monthly burn rate."*

## 📜 License

MIT — see [LICENSE](./LICENSE)

---

<sub>Part of the <a href="https://github.com/Dhanush-Aries">Dhanush Shankar</a> AI engineering portfolio.</sub>
