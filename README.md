# btc-cent-forecast-01

[![make.fun · btc-cent-forecast-01](https://make.fun/badge/btc-cent-forecast-01.svg)](https://make.fun/bounty/btc-cent-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=btc-cent-forecast-01)
[![rank](https://make.fun/badge/btc-cent-forecast-01/Endijuan33/btc-cent-forecast-01/rank.svg)](https://make.fun/bounty/btc-cent-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-cent-forecast-01)
[![reward](https://make.fun/badge/btc-cent-forecast-01/Endijuan33/btc-cent-forecast-01/reward.svg)](https://make.fun/bounty/btc-cent-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=btc-cent-forecast-01)

Forecast Bitcoin's US-dollar price 4 hours ahead, 12 times over 48 hours.
Entry for the make.fun bounty `btc-cent-forecast-01` ($250).

## Method

Damped short-horizon momentum, one parameter only:

```
forecast = last * exp(0.25 * meanLogRet60 * 240), clamped to +/-1% of last
```

- `meanLogRet60` = mean per-minute log return over the last 60 minutes of the
  case's 72 hours of 1-minute closes.
- The drift is extrapolated over the 240-minute horizon with a 0.25 damping
  factor, then capped at a 1% move from the last price.
- The result is kept on the price grid's 5 decimals and inside (0, 10,000,000).

Chosen on the kit's 6 practice cases (answers recovered from the next case's
checkpoint close): practice MAE **$334.91** vs the house persistence baseline's
**$470.55** (won on 4 of 5 scored cases). Mean reversion was tested and
consistently hurt; the 60-minute drift with damping 0.25 was the best simple
forecaster and the least overfit-prone (a single fixed parameter).

## Run

Node 22, standard library only, offline, deterministic:

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out node main.ts
```

Reads every `<id>.in` in the input directory, writes `<id>.out` as
`{"forecasts":[{"case":"<id>","price":<number>}]}`.

## License

MIT — see `LICENSE`.
