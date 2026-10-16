# Audit: do open-source trading bots actually make money?

Five repositories, checked against one question: **is there a verifiable profit here, or only a claim?**

Audited 2026-10-16. Star counts, descriptions and READMEs were read from the GitHub API on that date.
Nothing below is inferred from a blog post; every number is quoted from the repository itself.

---

## The criteria

Six things decide whether a "profitable" repo is evidence or advertisement:

1. **Is the claim specific?** A number with a period, or a vibe?
2. **Is it real money?** Backtest, dry-run, or funded account?
3. **Is there a benchmark?** Beating zero is not the same as beating holding the asset.
4. **Is friction modelled?** Fees, spread, slippage — at the size actually traded.
5. **Is there an out-of-sample result?** Or one number from the best parameter set?
6. **Is it a product or a funnel?** Deploy buttons, Telegram communities and referral links are
   revenue models in themselves.

---

## What the five actually say

### 1. [austin-starks/Public-Portfolio-Challenge](https://github.com/austin-starks/Public-Portfolio-Challenge) — 63 stars

The strongest case in the set, because it is the only one with **real money and a live feed**.

> *"4 AI agents. One runbook. Real $25K, live and verifiable. Currently **+22.85%**."*

The repository's own scoreboard, refreshed weekly by GitHub Actions from the live account API:

> | Account value | Total return | Return vs. SPY | Max drawdown | Days live |
> | ---: | ---: | ---: | ---: | ---: |
> | $27,703.50 | **+10.81%** | **−3.97 pp** (SPY +14.79%) | **−18.56%** | 217 |

**Finding:** the description advertises **+22.85%**; the live scoreboard in the same repository reports
**+10.81%**, and it **underperformed a passive S&P 500 index fund by 3.97 percentage points** while
carrying an **18.56% maximum drawdown**.

That is not fraud — the API is public and the data is real, which is more than almost anything else in
this space offers. It is something more useful: **a fully verifiable, honestly instrumented record that
still lost to an index fund.** Real money, real feed, 217 days, and the answer is "buying SPY did
better with less risk."

### 2. [freqtrade/freqtrade-strategies](https://github.com/freqtrade/freqtrade-strategies) — 5,554 stars

The largest strategy collection on GitHub, eight years old. Its README:

> *"These strategies are for educational purposes only. Do not risk money which you are afraid to lose.
> USE THE SOFTWARE AT YOUR OWN RISK. THE AUTHORS AND ALL AFFILIATES ASSUME NO RESPONSIBILITY FOR YOUR
> TRADING RESULTS."*

**Finding:** the most-cited "trading strategies" repository in existence **makes no profit claim at
all**, and explicitly disclaims responsibility for results. The profit claim is made by whoever
downloads it.

### 3. [jesse-ai/jesse](https://github.com/jesse-ai/jesse) — 8,652 stars

> *"Jesse is an advanced crypto trading framework that aims to simplify researching and defining
> **YOUR OWN** trading strategies for backtesting, optimizing, and live trading."*

**Finding:** 8,652 stars, actively developed (last push the day before this audit) — and **"YOUR OWN"
is in bold**. This is a framework. There is no strategy in it to audit, and no claim to check.

### 4. `edeng23/binance-trade-bot` — 14 stars at this path

Widely recommended across the web. What the API returns for that path today: **14 stars**, last push
February 2026, GPL-3.0.

**Finding (survivorship):** the version being recommended does not match the version that exists. The
premise is stated as self-evident rather than tested:

> *"all cryptocurrencies pretty much behave in the same way. When one spikes, they all spike... if coins
> are basically oscillating with respect to each other, it seems smart to trade the rising coin for the
> falling coin, and then trade back when the ratio is reversed."*

There is no friction model, no benchmark and no out-of-sample result — only a thesis. And the README
carries a **Heroku deploy button, a Telegram community link and the author's Twitter**: the classic
funnel shape, where the bot is the top of the funnel and the audience is the product.

### 5. [francisx1999/crypto-trading-bot-postmortem](https://github.com/francisx1999/crypto-trading-bot-postmortem) — the control

Not a profit claim. A negative result, and the most rigorous document in the set:

> *"Before I tested anything, I defined the bar: **net ≥ 1.5% per month, compounded, over a 24-month
> backtest at realistic fees.**"*

And critically, it says **why** that bar:

> *"a $2,000 wallet × 1.5% net per month = $30/month — barely enough to cover a $5 VPS, a $7.99 Claude
> subscription, and minor tooling. Anything less and the project is structurally underwater on costs."*

That is an **economic** gate, not a statistical one — the honest question isn't "does it make money" but
"does it make more than it costs to run." It also notes the market itself fell 13–18% over the window,
so clearing +36% means beating holding by ~50pp: *"a real edge claim, not a marketing one."* Real fee
tiers are used (Coinbase 0.4%/0.6%, Kraken 0.25%/0.40%).

Results across seven strategies:

- One hyperopt-optimized over 26 months: **reported** 75% win rate and 1.65% max drawdown →
  **out-of-sample total return −1.16%**, win rate 60%, **per-trade expected value −0.88%**
- Another: **−33.08%** and **−55.74%** on two variants, max drawdown 33.9% over 622 days, win rates
  51.1% / 41.1%
- **180 trades. 0 of 100 hyperopt epochs cleared the gate.**

> *"Tuning made it actively worse, because the trade-count-rewarding objective just told it to lose money
> faster."*

And the single most instructive table in the whole set — where the money actually went:

| exit reason | trades | win % | P&L |
|---|---:|---:|---:|
| ROI take-profit | 88 | **100%** | **+$740** |
| trailing stop | 4 | 100% | +$37 |
| **exit_signal (opposite EMA cross)** | **71** | **0%** | **−$970** |
| stop_loss | 17 | 0% | −$469 |

> *"The strategy is finding real trades. But the exit_signal logic fires 71 times across the test, every
> single one of those 71 is a loser, and they collectively bleed more than the wins capture."*

**Finding:** entries were fine. The **exit rule** destroyed the strategy. A 75%-win-rate backtest became
a −1.16% live-shaped result, and the loss was concentrated in a single rule that looked reasonable in
isolation.

---

## Scoreboard

| repo | stars | claims profit | real money | benchmark | friction | out-of-sample | verdict |
|---|---:|---|---|---|---|---|---|
| Public-Portfolio-Challenge | 63 | yes (+22.85%) | **yes, $25K** | SPY | live | 217 days | **Verifiable — and it underperformed SPY** |
| freqtrade-strategies | 5,554 | **no** | — | — | — | — | Framework assets, explicitly disclaimed |
| jesse | 8,652 | **no** | — | — | — | — | Framework. "YOUR OWN" is in bold |
| binance-trade-bot | 14 | thesis only | — | none | none | none | Untested premise + funnel |
| crypto-trading-bot-postmortem | — | **no** (negative) | — | BTC basket | **yes, real tiers** | **7 strategies** | **The only rigorous one, and it's a negative** |

**Of five repositories: zero hand you a profit. Four don't claim to. The one with a genuinely
verifiable record underperformed an index fund.**

---

## What this actually teaches

1. **The biggest repos are infrastructure, not edges.** 14,206 combined stars between freqtrade-strategies
   and jesse, and neither claims a single dollar of profit. The people who understand this best are the
   ones who refuse to claim.
2. **Verifiability is rare and precious — and it still isn't profitability.** The only repo here with a
   funded, live, API-readable account is also one that lost to SPY. If even the verifiable case fails
   the benchmark, the unverifiable ones are not worth reading.
3. **Backtest-to-live decay is brutal and predictable.** 75% win rate and 1.65% max drawdown became
   −1.16% out of sample. That gap is not bad luck; it is what hyperopt does.
4. **Losses concentrate in exits, not entries.** 71 exit-signal trades, 0 winners, −$970. If you take
   one thing from this audit, take that table.
5. **The economic gate is the honest one.** Not "is there an edge" but "does the edge exceed the cost of
   running the thing." For a $2,000 account that bar is ~1.5%/month, and almost nothing clears it.
6. **Star counts measure popularity, not profit.** The most-recommended bot in this set is a 14-star
   path with an untested thesis, and the most rigorous document in the set is a postmortem with almost
   no stars.

## What this does not do

This audit reads claims and checks them for **specificity, verifiability and method**. It has not
re-implemented any of these strategies, and it does not prove any of them unprofitable — it shows what
each repository documents about itself, and whether that documentation would survive review.

A strategy that loses in a backtest may still be a business. A strategy that wins in a backtest is not
a business until it wins with real money after fees.

## Related work

This audit is the companion to [solana-copy-trading-kill-test](https://github.com/ivanzoo3-14/solana-copy-trading-kill-test),
a pre-registered evaluation harness that asks the same question of copy-trading: does the measured edge
survive friction and out-of-sample selection? It returned a negative result, and the four defects found
in the instrument after the fact are published alongside it.

The same discipline, applied outward instead of inward.

## License

MIT for the text of this audit. Quoted material belongs to the repositories it came from.
