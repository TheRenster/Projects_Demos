# Projects & Demos

A collection of standalone data science and finance projects. This repo is linked
from my personal portfolio so visitors can browse the code behind two featured projects.

---

## Job Candidate Fit Analysis Tool

### What it does

Upload your resume (PDF or DOCX) and this tool scores it against 100 real developer
job postings from the Stack Overflow survey dataset. It uses BERT embeddings and cosine
similarity to measure how well your skills align with each role, ranks jobs by match
likelihood, and gives you concrete recommendations on which technologies to add to
close the gap.

### Why you might care

- See a practical example of NLP (BERT) applied to a real-world career problem
- Understand how semantic similarity works beyond simple keyword matching
- The output is genuinely useful: ranked job matches with salary and country context,
  plus skill gap recommendations

### Tech used

- `transformers` (BERT via HuggingFace) for semantic embeddings
- `scikit-learn` cosine similarity for scoring
- `PyPDF2` and `python-docx` for resume parsing
- Stack Overflow Developer Survey dataset (`stackoverflow_full.csv`)
- Runs in Google Colab (GPU recommended)

### How to run

1. Open `Job_Alignment_Analysis.ipynb` in Google Colab
2. Upload the Stack Overflow dataset when prompted
3. Upload your resume (PDF or DOCX)
4. Review your ranked job matches and skill gap recommendations

---

## Crypto Arbitrage Scanner

### What it does

Scans real-time exchange rates across 13 cryptocurrencies, builds a directed graph
of all possible trading paths, and identifies pricing disequilibrium — moments where
trading A -> B -> C -> A yields more than you started with. When a profitable path
exceeds a configurable threshold, it fires off concurrent market orders via the
Alpaca paper trading API.

### Why you might care

- See graph theory (NetworkX) applied to a finance problem
- Understand how triangular arbitrage works in crypto markets
- The order execution is real (paper trading) and uses concurrent threads to
  minimize slippage

### Tech used

- `networkx` for directed graph construction and path analysis
- `alpaca-trade-api` for paper trading order execution
- CoinGecko API for live exchange rate data
- `concurrent.futures` for parallel order submission

### Coins tracked

BTC, ETH, LTC, BCH, DOGE, SHIB, AVAX, DOT, AAVE, LINK, MKR, UNI, XTZ

### How it works

1. Fetches live rates for all coin pairs from CoinGecko
2. Builds a weighted directed graph of exchange rates
3. Enumerates all simple trading paths between coin pairs
4. Calculates the round-trip product (forward x reverse) for each path
5. If any path exceeds the threshold (default: 0.02%), places concurrent
   market orders via Alpaca

> **Note:** The API keys in the source file are paper trading keys tied to a
> demo account. Do not use this in a live trading environment without replacing
> credentials and adding proper risk controls.
