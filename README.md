# Nova risk control panel: static demo

A static, permanent demo of an agentic AI prototype for supply chain risk management.

**Live demo:** https://shubham888999.github.io/nova-risk-demo/
**Archived version:** [https://doi.org/10.5281/zenodo.24540378](https://doi.org/10.5281/zenodo.24540378)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24540378.svg)](https://doi.org/10.5281/zenodo.24540378)

## What this is

Nova Electronics is a fictional company in Chicago. It buys a controller module from Busan, Manila and Mexico City, and a battery pack from Singapore. News arrives day by day from 27 October to 11 November 2026, including a port strike at Busan.

For each event, the prototype does the following:

1. It reads the news.
2. It decides which risk method fits: CVaR, VaR, mean variance, Monitor, Abstain or Close.
3. It computes the risk with a deterministic engine.
4. It verifies the result.
5. It explains the result.
6. It waits for a manager's decision.

Language models handle language only. Every number comes from the engine.

## What is live and what is recorded

- Every number on the page was computed in advance by the R risk engine in `prototype/` and saved in `data.js`. That includes every Risk lab setting and every What-if explorer combination.
- Text from the AI agents (the monitoring, scenario and explanation agents) is the recorded output of `openai/gpt-oss-120b` from the prototype's runs, stored in `prototype/cache/`. Where no output was recorded for a day, the page says so.
- The page calls no language model, server or external service. It is plain HTML, CSS and JavaScript with no external libraries or fonts. It works offline: open `index.html` in a browser.
- All data is synthetic.

## Repository contents

| Path | Contents |
|---|---|
| `index.html`, `data.js` | The static demo |
| `prototype/R/` | Risk engine and agents: routing, duration model, scenarios, CVaR linear programme, verification, monitoring, scenario and explanation agents |
| `prototype/app.R` | The full interactive prototype (R Shiny). Live AI features need an API key in the environment (see `prototype/R/llm.R`). It also runs offline from the recorded outputs |
| `prototype/data/` | Synthetic company data (`Nova_Demo_Data.xlsx`) and the map outline |
| `prototype/cache/` | Recorded agent outputs |
| `prototype/export.R` | Regenerates `data.js` from the engine |

## Reproducing the numbers

You need R 4.3 or later with the packages `readxl`, `jsonlite`, `lpSolve` and `httr`. From the repository root, run:

```
Rscript prototype/export.R prototype .
```

This reruns the engine for every day, setting and combination, and rewrites `data.js`. No API key is needed, because agent outputs are replayed from `prototype/cache/`.

## Citation

Deshpande, S., Sarkar, P., and Gunasekaran, A. (2026). *Nova risk control panel: static demo of an agentic AI prototype for supply chain risk management* (Version 1.0.0). Zenodo. https://doi.org/10.5281/zenodo.24540378

See also `CITATION.cff`.

## License

Code: MIT License (see `LICENSE`). The synthetic data and recorded outputs may be reused with attribution.
