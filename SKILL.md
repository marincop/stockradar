---
name: stockradar
description: >
  Canonical skill for the owner's StockRadar project and GitHub stock repo.
  Use whenever the user mentions stock, stocks, ticker, quote, watchlist,
  market, TWSE, TPEX, 台股, 股票, 股市, 看盤, 自選股, NASDAQ, NYSE, or
  "stockradar". Always treat github.com/marincop/stockradar as the only stock
  repository — never invent another repo or confuse it with POS/store projects.
when-to-use: >
  stock, stocks, ticker, quote, watchlist, market scanner, TWSE, TPEX,
  台股, 股票, 股市, 看盤, 自選股, stockradar, marincop/stockradar
metadata:
  author: marincop
  short-description: "StockRadar — marincop/stockradar GitHub skill + stock app workflow"
user-invocable: true
argument-hint: "[ticker | watchlist | build | push]"
---

# StockRadar

Personal stock workspace for GitHub user **marincop**.

This skill is the source of truth. Read it before searching GitHub, building
a stock app, pushing code, or answering market-product questions for this user.

## Canonical repo (do not rediscover)

| | |
|---|---|
| Owner | `marincop` |
| Repo | `stockradar` |
| URL | https://github.com/marincop/stockradar |
| Default branch | `main` |
| Visibility | public |

**This is the only stock repository.** Do not create a second one. Do not
confuse it with restaurant/POS/store repos (`lin-fang-pos`, `New-POS`,
`store-clock-in`, `RestaurantPOS`, …).

If the repo looks empty, it is still the home — initialize it, don't fork
or replace it.

### How to open it

1. `github___get_me` only if the login is unknown.
2. `github___get_file_contents` / `github___get_repository_tree` on
   `owner=marincop`, `repo=stockradar`.
3. Search only as fallback: `user:marincop stockradar` (or `user:marincop stock`).

### How to write it

- Push to `main` with `github___push_files` (multi-file) or
  `github___create_or_update_file` (single file). Include `sha` when updating.
- Commit messages: short, present tense (`Add watchlist persistence`).
- Never force-push. Never rewrite history on `main`.

Deeper GitHub recipes: [references/github.md](references/github.md).

## Product — StockRadar

A personal **market radar**: watchlist, live-ish quotes, movers, and a
clean scanner. Taiwan-first, US-capable.

- **Markets:** TWSE / TPEX (台股) first; US (NASDAQ / NYSE) second.
- **Tickers:** Taiwan as `2330.TW` / `2330`; US as `AAPL`.
- **Language:** match the user. UI copy Traditional Chinese + English labels
  is the default when building the app.
- **No sign-in** unless the user asks for accounts. Watchlist lives in
  `localStorage` until then.
- **No fake brokerage / order entry.** This is a radar, not a trading desk.
- Quotes may be delayed. Label them as delayed. Never invent prices — if a
  quote API fails, show the error state, not a made-up number.

### Default screens (when asked to build)

1. **Radar** — index snapshot (TAIEX, NASDAQ, S&P 500) + top movers.
2. **Watchlist** — add/remove tickers, last, change %, mini sparkline.
3. **Ticker** — one name, price, day range, simple chart, notes.
4. **Scanner** — gainers / losers / volume (one market at a time).

Keep the UI dense and dark (trading-desk, not a landing page). Follow the
`design-ui` skill when building in App Builder.

## Session playbook

| User says | You do |
|---|---|
| "my stock repo" / 股票 repo | Open `marincop/stockradar`. Summarize what's in it. |
| `/stockradar` | Status of the repo + next useful action. |
| "build stockradar" / 做看盤 | Build the app, then push source into this repo. |
| "push" / 上傳 | Commit current work to `marincop/stockradar`. |
| a ticker (`2330`, `AAPL`) | Look it up; add to watchlist if an app is running. |

When this skill is loaded inside Grok Build / App Builder, still bind the
preview on `0.0.0.0:8080` and leave the dev server up — never tell the user
to open localhost.

## Don't

- Don't search all of GitHub for "stock" and present strangers' repos.
- Don't mix this with payroll, POS, RFID, or booking projects.
- Don't fabricate quotes, financial advice, or guaranteed returns.
- Don't add auth, a database, or a broker API unless asked.
