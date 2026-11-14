# Tennis Scraper

![Tennis Scraper](https://raw.githubusercontent.com/smoldesk/apify-scrapers/main/assets/tennis/banner.webp)

Scrape live tennis scores, results, upcoming matches, betting odds, head-to-head and ATP/WTA rankings. ATP, WTA, Challenger and ITF. No login. Runs on [Apify](https://apify.com/smoldesk/tennis-scraper).

## What you get

- **Live scores**: `matchStatus: "live"` returns every match in play (ATP/WTA tour, Challenger, WTA 125, UTR) with game points, server and win probability, joined to the pre-match odds.
- **Matches**: date, status, tournament, round, surface, players, seeds, score, set scores and winner.
- **Odds**: closing odds for both players and the implied probability.
- **Match details** (optional): odds from every bookmaker, H2H, player bios, odds history and Over/Under, Asian Handicap and Correct Score markets.
- **Players**: age, height, weight, handedness, current and highest rank, win-loss by surface and year.
- **Rankings**: ATP and WTA singles, doubles and Race, for any date.
- **Filters**: date range, tour and match type, level (tour, Challenger, ITF, UTR), tournament name, player name, finished or upcoming.

## Run it

Open the [Tennis Scraper on Apify](https://apify.com/smoldesk/tennis-scraper), fill in the form and click Start. Or call it from code with your [Apify token](https://console.apify.com/settings/integrations):

```bash
curl -X POST "https://api.apify.com/v2/acts/smoldesk~tennis-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "startDate": "2026-10-01",
    "endDate": "2026-10-18",
    "matchTypes": ["atp-single"],
    "levels": ["tour"],
    "matchStatus": "finished",
    "includeMatchDetails": true,
    "rankings": ["atp-singles"],
    "rankingTopN": 50
  }'
```

## Sample output

```json
{
  "type": "match",
  "date": "2026-10-18",
  "startTimeUtc": "2026-10-18T08:40:00Z",
  "status": "scheduled",
  "tour": "ATP",
  "level": "tour",
  "tournament": "Shanghai",
  "round": "final",
  "surface": "hard",
  "player1": "Davidovich Fokina A.",
  "player1Seed": "25",
  "player2": "Jodar R.",
  "player2Seed": "12",
  "oddsPlayer1": 2.12,
  "oddsPlayer2": 1.72,
  "impliedProbPlayer1": 0.4479
}
```

```json
{
  "type": "ranking",
  "ranking": "ATP singles",
  "rankingDate": "2026-10-05",
  "rank": 1,
  "movement": 0,
  "player": "Sinner Jannik",
  "country": "Italy",
  "points": 11000
}
```

Export as JSON, CSV or Excel, or pipe it into Google Sheets, Make, Zapier or n8n.

## Pricing

Pay per result. No monthly fee. Prices drop on paid Apify plans.

| Result (per 1,000) | Free | Starter | Scale | Business |
|---|---|---|---|---|
| Match | $2.50 | $2.00 | $1.70 | $1.40 |
| Match details add-on | +$3.50 | +$3.00 | +$2.50 | +$2.00 |
| Player profile | $3.50 | $3.00 | $2.50 | $2.00 |
| Ranking row | $0.60 | $0.50 | $0.40 | $0.30 |

## Limits

- No live score for ITF matches. Live runs are snapshots: schedule them every few minutes.
- Retirements are inferred from an unfinished last set, so a few can show as `finished`.
- H2H is the record at the time you scrape, not at the time of the match.
- Odds history is thin before about 2009 and for low-level ITF matches.

## FAQ

**Is there a free tennis odds API?**
Not really. Official ATP and WTA data and most odds APIs are paid. This reads public TennisExplorer pages and charges per result.

**Can I get historical tennis results with odds?**
Yes. Set `startDate` and `endDate`. Results go back to the early 2000s and odds to about 2009.

**Can I get live tennis scores?**
Yes. Set `matchStatus` to `live`. Each match in play has the score, current game points, server and win probability, plus the pre-match odds. ITF is not covered live.

**How do I get one tournament, like Wimbledon?**
Paste the tournament URL in `tournamentUrls`, or set dates with `tournamentNames: ["Wimbledon"]`.

**Does it include Challenger and ITF matches?**
Yes. Use `levels` to pick `tour`, `challenger`, `itf` or `utr`.

**How do I get head-to-head records?**
Set `includeMatchDetails` to true. Each match then carries H2H and odds from every bookmaker.

## More scrapers

Tennis is one of 21 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
