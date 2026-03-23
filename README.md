# Program KPI & Marketing Budget Calculator

A self-contained, browser-based tool for planning marketing KPIs, allocating budgets across geographies and channels, and pooling resources across multiple partners.

## Quick Start

1. Open `goodwall-kpi-calculator.html` in any modern browser.
2. That's it. No install, no build, no server.

## What It Does

The calculator models a five-stage conversion funnel:

**Reach** → **Accelerated** → **Engaged** → **Trained** → **Credentialed**

It provides three working phases:

| Phase | Purpose |
|---|---|
| **KPI Planning** | Calculate achievable KPIs from a budget, or determine the budget required to hit a KPI target. Split by geography with editable benchmarks. |
| **Channel Strategy** | Allocate budget across marketing channels (platforms, ad types). See how each channel contributes to the funnel. |
| **Partner Marketing Pool** | Combine multiple partners' budgets by geography and KPI priority. View pooled projections. |

## Features

- **Two calculation modes:** Budget → KPIs (forward) or KPI Target → Budget (reverse)
- **Geographic targeting:** Add unlimited geographies with per-region CPI and reach multipliers
- **Editable benchmarks:** All conversion rates are inline-editable
- **Dynamic channels:** Add custom platforms and ad types with per-channel CPI and target stage
- **Partner pooling:** Multi-partner budget aggregation by geography
- **Auto-save:** All inputs persist in `localStorage`
- **CSV export:** Download current phase data as `.csv`
- **Responsive:** Works on desktop and tablet
- **Print-ready:** All phases render for printing

## Requirements

- Any modern browser (Chrome, Firefox, Safari, Edge)
- Internet connection for Google Fonts and Phosphor Icons (falls back to system fonts offline)

## File Structure

```
goodwall-kpi-calculator.html   # The complete application (single file)
README.md                      # This file
wiki-calculator-overview.md    # Detailed documentation (Wiki page)
```

## Hosting

### Local Use
Double-click the HTML file to open it in your default browser.

### Static Hosting
Upload to any static host:
- **GitHub Pages:** Push to a repo, enable Pages in Settings
- **Netlify:** Drag and drop the file at [app.netlify.com/drop](https://app.netlify.com/drop)
- **Vercel:** `vercel deploy` from the directory
- **Any web server:** Place the file in your document root

### Google Sites Embedding
1. Host the file at a public URL (see above)
2. In Google Sites: **Insert → Embed → By URL**
3. Paste the hosted URL

> Google Sites does not support pasting full HTML pages into the embed code box. You must use the URL method.

## Customization

All data is editable directly in the UI:

- **Geographies:** Name, budget allocation %, CPI, reach multiplier
- **Benchmarks:** Accelerated→Engaged, Engaged→Trained, Trained→Credentialed rates
- **Channels:** Name, platform, ad type, budget %, CPI, target funnel stage
- **Partners:** Name, budget, geographic focus (multi-select), KPI priority

To customize default values, edit the JavaScript constants at the top of the `<script>` block:
- `GEO_PRESETS` — Default geographies
- `DEFAULT_BENCHMARKS` — Default conversion rates
- `DEFAULT_CHANNELS` — Default channel configuration
- `DEFAULT_PARTNERS` — Default partner list

## How the Math Works

### Forward (Budget → KPIs)

```
For each geography:
  Budget_geo       = Total Budget × Allocation%
  Accelerated_geo  = (Budget_geo / CPI_geo) × Organic Boost
  Reach_geo        = Accelerated_geo × Reach Multiplier
  Engaged_geo      = Accelerated_geo × Benchmark(A→E)
  Trained_geo      = Engaged_geo × Benchmark(E→T)
  Credentialed_geo = Trained_geo × Benchmark(T→C)

Totals = sum across all geographies
```

### Reverse (KPI Target → Budget)

```
Accelerated needed = Target / (product of conversion rates from Accelerated to target stage)
Blended efficiency = Organic Boost × Σ(Allocation_i / CPI_i)
Required Budget    = Accelerated needed / Blended efficiency
```

## Privacy

All data stays in your browser. No analytics, no tracking, no server calls. The only external requests are for fonts (`fonts.googleapis.com`) and icons (`unpkg.com`).

## License

Internal tool. Modify and redistribute as needed within your organization.
