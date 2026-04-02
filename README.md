# Anxiety Index

**Workplace Stress Intelligence Platform**

https://dstratonov.github.io/anxiety-index/

Anxiety Index scores IT companies on a 0-100 scale based on how stressful they are to work at. Scores are derived from public employee reviews, news articles, and workplace data — gathered and analyzed weekly by AI using live web search.

## How It Works

Every week, an automated pipeline:

1. **Discovers** the top ~100 IT companies via web search
2. **Researches** each company — layoffs, compensation, hiring process, culture, career growth
3. **Scores** each company across 5 weighted criteria using Claude AI
4. **Deploys** updated results to the live site

## Scoring Criteria

| Criterion | Weight | What It Measures |
|---|---|---|
| Stability | 20% | Layoffs, financial health, leadership turnover |
| Compensation | 20% | Pay fairness, benefits, equity practices |
| Hiring Process | 10% | Interview experience, ghosting, bait-and-switch |
| Work Atmosphere | 30% | Work-life balance, management quality, culture |
| Career Growth | 20% | Promotions, learning opportunities, internal mobility |

**Anxiety Level** = weighted average of all criteria (0-100, higher = worse)

### Verdict Scale

- **CRITICAL** (80-100) — Severe workplace issues
- **HIGH** (60-79) — Significant concerns
- **ELEVATED** (40-59) — Mixed signals, some issues
- **LOW** (0-39) — Generally positive workplace

## Data Freshness

- Only data from the **last 2 years** is considered
- Last 6 months: full weight
- 6-12 months: 75% weight
- 1-2 years: 50% weight
- Scores refresh weekly via automated pipeline

## Tech Stack

- **Frontend**: React 18, Vite 5, CSS-in-JS
- **Scoring Pipeline**: Node.js, Claude API with web search
- **Hosting**: GitHub Pages (auto-deployed)
- **Automation**: GitHub Actions (daily cron)

## Project Structure

```
src/                    React frontend
  components/           UI components (gauge, cards, filters)
  data/companies.js     Auto-generated company data
pipeline/               Scoring pipeline
  discover.js           Find top IT companies via web search
  batch-score.js        Score companies in daily batches
  prompts.js            Claude scoring instructions & rubrics
  score.js              Claude API integration with web search
  build-frontend-data.js  Generate frontend data from results
  companies.json        Current company list
  results.json          Accumulated scoring results
.github/workflows/      GitHub Actions automation
```

## Running Locally

```bash
# Frontend
npm install
npm run dev             # Opens at http://localhost:3000

# Pipeline (requires ANTHROPIC_API_KEY)
cd pipeline
npm install
node discover.js --count 100
node batch-score.js --batch-size 15
node build-frontend-data.js
```

## Automation Schedule

- **Monday 06:00 UTC**: Discover companies + score first batch
- **Tuesday-Sunday 06:00 UTC**: Score next batch of ~15 companies
- Each run rebuilds and redeploys the site

## License

MIT
