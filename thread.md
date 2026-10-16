# X thread -- paste-ready

Post as a thread. Plain text: X does not render markdown. Every post below is under 280 characters
including the URL rule (any link counts as 23 regardless of its real length).

---

**1/**

I audited the 5 most-recommended open-source trading bots on GitHub.

Question: is there a verifiable profit, or only a claim?

Zero of them hand you a profit.
Four don't even claim to.
The one with real money lost to an index fund.

---

**2/**

The two biggest strategy repos: 14,206 stars between them.

- freqtrade-strategies -- "educational purposes only... no responsibility for your trading results"

- jesse -- "define YOUR OWN trading strategies"

Neither claims a dollar. The people who get this refuse to claim.

---

**3/**

The only repo with a funded, live, API-readable account: Public-Portfolio-Challenge, real $25K.

Its description says +22.85%.
Its own live scoreboard says +10.81%.
vs SPY: -3.97 points. Max drawdown: -18.56%.

Real money. Real feed. Index fund won.

---

**4/**

The bot everyone recommends, binance-trade-bot, shows 14 stars at its path today. Its premise is untested: "trade the rising coin for the falling coin."

No friction model. No benchmark. No out-of-sample test.

It does have a deploy button, a Telegram group and a Twitter link.

---

**5/**

One repo in the set is honest, and it's the most rigorous: crypto-trading-bot-postmortem.

7 strategies, 24 months, real fee tiers. Kill gate: net >= 1.5%/month -- chosen because $2,000 x 1.5% barely covers a $5 VPS.

Result: 0 of 100 hyperopt epochs cleared it.

---

**6/**

Worth more than the other four repos combined:

ROI take-profit:  88 trades, 100% win, +$740
trailing stop:     4 trades, 100% win, +$37
exit_signal:      71 trades,   0% win, -$970
stop_loss:        17 trades,   0% win, -$469

Entries were fine. One exit rule destroyed it.

---

**7/**

And the decay nobody advertises:

A strategy hyperopt-optimized over 26 months reported 75% win rate and 1.65% max drawdown.

Out of sample: -1.16% return, -0.88% expected value per trade.

That gap isn't bad luck. That's what optimization does.

---

**8/**

Five things it taught me:

- Stars measure popularity, not profit
- Verifiable != profitable
- Losses concentrate in exits, not entries
- The honest gate is economic: beat the cost of running it
- "Educational purposes only" is the most truthful line in open-source trading

---

**9/**

Companion to my last project, which asked the same question about copy-trading and also came back negative.

I publish negative results because they're the only ones I can verify.

Full audit:
github.com/ivanzoo3-14/trading-bot-audit