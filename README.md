# token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/jhm0617/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/jhm0617/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

A radar for token launches that have not happened yet: every pre-token protocol in the sealed DefiLlama snapshot, ranked by an implied value derived from its own figures, each with a concrete farm plan.

## The model (radar-2)

Implied value is not a flat multiple of TVL. The category multiple is read off the snapshot itself: the median market-cap-per-TVL of the live-token protocols in the same category (at least 3 of them), else the global median, clamped to [0.05, 1.20]. Then:

```
implied = round(tvl_usd
  x categoryMultiple
  x (1 + clamp(change_7d, -40, 80) / 100 x 0.5)
  x (0.70 + 0.30 x min(age_days, 1460) / 1460)
  x (0.90 + 0.10 x min(chains, 10) / 10))
```

The board covers all 40 watchlist protocols plus every rankable pre-token protocol below the $50M floor (178 rows in all). Live-token protocols are set aside with their market caps shown, never mixed into the ranking. A protocol is shown as pre-token because its record carries no token; that is not proof it has none.

## Run it

```sh
MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=output node main.ts
```

`main.ts` reads `snapshot.json`, writes `board.json`, `data.js`, `dashboard/` and `screenshots/` to the output directory, and `dossier.json` last. The dashboard is a static page with no network: open `output/dashboard/index.html` in a browser.

---

<sub>Entered on [make.fun](https://make.fun/?ref=wnpng6sv&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
