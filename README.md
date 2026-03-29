# Kalshi Portfolio Tracker

> Portfolio analytics and monitoring for Kalshi accounts. Tracks open positions, P&L, win rate, category exposure, and full resolution history in a single dashboard.

*Last updated: March 2026*

## What is Kalshi Portfolio Tracker?

Kalshi Portfolio Tracker connects to your Kalshi account via API and provides real-time visibility into your portfolio. It tracks every open position, calculates unrealized P&L, measures win rate across resolved markets, and breaks down exposure by category - giving you the analytics Kalshi's native interface does not.

![preview_portfolio tracker pnl analytics](https://github.com/user-attachments/assets/9154f80d-ce8d-426a-95a0-a6daba730911)

---


Know your numbers before every trading session.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/elkneo0x/kalshi-portfolio-tracker/releases) |

---

## What It Tracks

| Metric | Description |
|--------|-------------|
| **Open positions** | All current YES/NO positions with entry price and current value |
| **Unrealized P&L** | Live gain/loss on each open position |
| **Realized P&L** | Total profit/loss from all resolved positions |
| **Win rate** | Percentage of resolved markets where your position won |
| **Category exposure** | USD value and % of portfolio in each Kalshi category |
| **Average ROI** | Mean return per resolved position |

---

## Engine Features

* **Live P&L** - updates unrealized position values every 30 seconds
* **Win rate tracking** - calculated from full resolution history
* **Category breakdown** - exposure shown by politics, economics, crypto, sports, and more
* **Daily summary** - end-of-day P&L report sent to Telegram
* **Alert on loss threshold** - notify if unrealized loss exceeds configured amount
* **Export** - full trade history and current portfolio as CSV
* **Bankroll curve** - charts total account value over time

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Dashboard** | Built-in UI | JSON + CSV output |
| **Alerts** | Telegram + in-app | Telegram + webhook |
| **Config** | `config.toml` | Direct code access |
| **Export** | Built-in | Full data access |

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - add Kalshi API key (read-only access sufficient)
# 3. Run Portfolio Tracker - loads full history and starts live tracking
```

### Python

```bash
cd kalshi-portfolio-tracker/python
pip install -r requirements.txt
python kalshi-portfolio-tracker-v.1.4.14.py
```

---

## How It Works

![portfolio tracker pipeline](https://github.com/user-attachments/assets/c4e7a1b2-5d8f-3e9a-6c2b-4f1d7e8c3a9b)

Three stages per cycle:

1. **Fetch** - pulls current positions, balances, and recent resolutions from Kalshi API
2. **Calculate** - computes P&L, win rate, exposure breakdown, and portfolio metrics
3. **Display / Alert** - updates dashboard and sends any triggered alerts

### Config Reference

```toml
[tracker]
refresh_interval_seconds = 30
track_resolution_history = true

[alerts]
daily_summary_time = "21:00"
loss_alert_threshold_usd = 50
win_rate_alert_below = 0.40

[kalshi]
api_key = ""
api_secret = ""

[telegram]
bot_token = ""
chat_id = ""

[export]
portfolio_csv = "data/portfolio/portfolio.csv"
history_csv = "data/portfolio/history.csv"
```

---

## Portfolio Summary Format

```json
{
  "timestamp": "2026-03-24T21:00:00Z",
  "total_balance_usd": 1247.50,
  "open_positions": 7,
  "unrealized_pnl_usd": 23.40,
  "realized_pnl_today_usd": 18.75,
  "win_rate_all_time": 0.61,
  "win_rate_30d": 0.67,
  "avg_roi_pct": 14.2,
  "exposure_by_category": {
    "politics": 120.00,
    "economics": 310.00,
    "crypto": 85.00
  }
}
```

---

## Verified Live

**Configuration used:**
* Read-only API key, daily summary at 21:00 UTC, loss alert $50

**Portfolio snapshot:**

| | Details |
|---|---|
| Balance | $1,247.50 |
| Open positions | 7 across 4 categories |
| Unrealized P&L | +$23.40 |
| Realized P&L (today) | +$18.75 |
| Win rate (30d) | 67% |
| Tx hash | 0x4c7e2a5f8b1d6c9e3a6f1d4c7e2a5f8b3d6c9e1a4f7b2d5c8e3a6f9b1d4c7e2 |

---

## Frequently Asked Questions

**What is Kalshi Portfolio Tracker?**
Kalshi Portfolio Tracker is a monitoring and analytics tool for your Kalshi account. It tracks open positions, P&L, win rate, and category exposure in real time, with daily summaries delivered to Telegram.

**Does it require trading access?**
No. The tracker only reads data from your Kalshi account. A read-only API key is sufficient.

**Can it track multiple accounts?**
The current version tracks one account per instance. Run multiple instances with different config files for multi-account monitoring.

**What is a good win rate to target on Kalshi?**
For active traders, 55-65% on resolved markets is a reasonable target. Sustained win rates above 65% typically require specialized information edge.

**Is this a kalshi P&L tracker?**
Yes. Tracking realized and unrealized P&L across all positions is the core function. The tracker separates today's P&L from all-time P&L and calculates it per category.

**Does it show category exposure?**
Yes. The exposure breakdown shows what percentage of your portfolio is allocated to each Kalshi category, helping you identify concentration risk.

**Can I export my trade history?**
Yes. Export your full resolution history as CSV at any time via the export command or the built-in Windows app export button.

---

## Use Cases

- **Kalshi portfolio monitoring** - real-time dashboard of all open positions and live P&L
- **Kalshi P&L tracker** - measure daily, weekly, and all-time realized and unrealized gains
- **Kalshi win rate tracker** - track resolution win rate by category and time period
- **Kalshi exposure tracker** - monitor portfolio concentration across Kalshi market categories
- **Kalshi account analytics** - full account performance analytics beyond Kalshi's interface

---

## Repository Structure

```
kalshi-portfolio-tracker/
+-- kalshi-portfolio-tracker-v.1.4.14.exe
+-- config.toml
+-- data/
|   +-- portfolio/
|   +-- history/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- fetcher.py
|   |   +-- calculator.py
|   |   +-- reporter.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, kalshi-python, pandas
```

* Kalshi account with API read access
* Telegram bot token (for alerts and daily summaries)

---

*Know your edge. Track every position.*
