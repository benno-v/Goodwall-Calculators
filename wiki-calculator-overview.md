# Program KPI & Marketing Budget Calculator

## Overview

The **Program KPI & Marketing Budget Calculator** is a self-contained, browser-based tool for planning, budgeting, and coordinating marketing campaigns across programs. It helps operations teams translate business objectives into actionable KPI targets, allocate budgets across geographies and channels, and pool resources across multiple partners.

The calculator is a single HTML file with no server-side dependencies. Open it in any modern browser to get started.

---

## Core Concepts

### The KPI Funnel

The calculator models a five-stage conversion funnel, from broad awareness down to verified outcomes:

| Stage | Description |
|---|---|
| **Reach** | Total number of unique people exposed to program content, messaging, or branding through any channel (digital, in-person, media). Measures awareness and top-of-funnel exposure. |
| **Accelerated** | All installs + engagements. Users who installed the app or actively engaged with content as a direct result of marketing. |
| **Engaged** | Number of engagements on the platform, including posts, comments, likes, shares, clicks on banners/CTAs, survey/quiz responses, and content consumption. |
| **Trained** | Users who viewed educational content (>1 second) OR completed a quiz OR survey OR participated in a challenge. |
| **Credentialed** | Users who earned a credential, badge, or certificate demonstrating verified skill acquisition (completed a course module or full course). |

Each stage converts into the next at a configurable **benchmark rate**. The tool calculates all downstream stages automatically when you change any input.

### Key Variables

| Variable | What it controls |
|---|---|
| **Total Budget** | The total marketing spend available for the program. |
| **Primary KPI** | The funnel stage the program cares most about (highlighted throughout). |
| **Organic Boost Multiplier** | A multiplier applied to paid acquisition to account for organic/viral growth (e.g., 1.48 = 48% additional organic lift). |
| **CPI (Cost Per Install)** | The cost to acquire one Accelerated user in a given geography. This is the core economic input per region. |
| **Reach Multiplier** | How many people are reached per Accelerated user (e.g., 100 = for every install, 100 people saw the ad). |
| **Conversion Benchmarks** | Rates for Accelerated → Engaged, Engaged → Trained, and Trained → Credentialed. |

---

## Phases

The calculator is organized into three independent phases. You can use them sequentially or jump to any phase directly.

### KPI Planning

**Purpose:** Determine what KPI outcomes a given budget can achieve, or what budget is required to hit a specific KPI target.

**Two calculation modes:**

1. **Budget → KPIs**: Enter a total marketing budget. The calculator distributes it across geographies using allocation percentages, applies each geography's CPI and benchmarks, and shows the projected funnel outcomes.

2. **KPI Target → Budget**: Enter a target value for any funnel stage (e.g., "10,000 Credentialed"). The calculator works backward through the funnel and geography economics to determine the required budget.

**Geographic Targeting:**
- Add any number of geographies (countries, regions, or custom segments).
- Each geography has its own CPI, Reach Multiplier, and budget allocation percentage.
- The tool warns you if allocations don't sum to 100%.
- All benchmarks and allocations are editable inline.

**Outputs:**
- Summary cards showing total budget, primary KPI value, and cost per primary KPI.
- A visual funnel bar chart with conversion rates between stages.
- A detailed table with count, conversion rate, and cost-per-user for each stage.
- A geographic breakdown showing projected outcomes per geography.

---

### Channel Strategy

**Purpose:** Define the marketing channels and ad types that will deliver the KPI targets from the planning phase.

**Features:**
- Add any number of channels with fully editable fields: name, platform, ad type, budget percentage, CPI, and target funnel stage.
- Each channel can target a different funnel stage (e.g., Meta Ads target Accelerated, Community Outreach targets Reach).
- Budget allocation bar shows how spend is distributed across channels.
- Channel contribution funnel shows how each channel feeds into the overall KPI funnel, cascading through downstream stages using the benchmarks.

**Pre-populated examples include:**
- Meta Ads (App Install Campaign)
- Google UAC (Universal App Campaign)
- TikTok Ads (App Install)
- In-App Banners (Banner/CTA)
- Community Outreach
- Influencer Marketing

All examples are fully editable and removable. Add new channels with custom platforms and ad types.

---

### Partner Marketing Pool

**Purpose:** Combine budgets from multiple partners into a shared marketing pool, allocate by geography, and project combined outcomes.

**Features:**
- Add partners with their individual budgets, geographic focus areas, and KPI priorities.
- Geographic focus is multi-select — each partner can target multiple regions.
- Budget is split equally across a partner's selected geographies (can be adjusted by adding the same partner multiple times with different allocations).
- Pool by Geography table shows total budget, number of contributing partners, and percentage of pool per geography.
- Combined KPI projections show the pooled funnel outcomes with cost-per-user at each stage.

**Outputs:**
- Total pool budget and average budget per partner.
- Number of geographies covered.
- Per-geography budget pool with estimated Accelerated, Trained, and Credentialed users.
- Combined funnel visualization and KPI summary cards.

---

## How the Math Works

### Budget → KPIs (Forward Calculation)

For each geography:

```
Budget_geo = Total Budget × (Allocation% / 100)
Accelerated_geo = (Budget_geo / CPI_geo) × Organic Boost
Reach_geo = Accelerated_geo × Reach Multiplier_geo
Engaged_geo = Accelerated_geo × (Accelerated→Engaged %)
Trained_geo = Engaged_geo × (Engaged→Trained %)
Credentialed_geo = Trained_geo × (Trained→Credentialed %)
```

Totals are the sum across all geographies.

### KPI Target → Budget (Reverse Calculation)

1. Determine how many Accelerated users are needed to hit the target:
   - If target is Credentialed: `Accelerated = Target / (A→E% × E→T% × T→C%)`
   - If target is Trained: `Accelerated = Target / (A→E% × E→T%)`
   - If target is Engaged: `Accelerated = Target / A→E%`
   - If target is Accelerated: `Accelerated = Target`
   - If target is Reach: `Accelerated = Target / Weighted Reach Multiplier`

2. Calculate the blended cost efficiency across geographies:
   ```
   Accel per Dollar = Organic Boost × Σ(Allocation_i% / CPI_i)
   ```

3. Required Budget = Accelerated Needed / Accel per Dollar

### Partner Pool Calculation

Each partner's budget is divided equally across their selected geographies. For each geography, the pooled budget is then run through the same forward calculation using that geography's CPI and benchmarks.

---

## Data Persistence

All inputs are automatically saved to the browser's `localStorage`. Closing and reopening the page restores your last state. Use the **Reset** button to return to default values.

> **Note:** Data is stored per-browser. Different browsers or incognito/private windows will have separate saved states.

---

## Export

Click **Export CSV** in the header to download the current phase's data as a `.csv` file. The export includes:

- **KPI Planning:** Funnel summary with counts, conversion rates, and cost-per-user; geographic breakdown.
- **Channel Strategy:** Channel details with budget allocations, CPIs, and estimated users.
- **Partner Pool:** Partner details with budgets, geographies, and KPI priorities.

---

## Customization

### Adding Geographies

Click **Add Geography** in the KPI Planning phase. Set the name, allocation percentage, CPI, and Reach Multiplier for your market.

**Typical CPI ranges by market:**
| Market Type | CPI Range |
|---|---|
| Tier 1 (US, UK, EU) | $2.00 – $5.00 |
| Tier 2 (Brazil, South Africa) | $0.40 – $1.00 |
| Tier 3 (Nigeria, Kenya, India) | $0.10 – $0.50 |
| Southeast Asia | $0.10 – $0.40 |

### Adjusting Benchmarks

Conversion benchmarks are editable in the **Conversion Benchmarks** table on the KPI Planning phase. Changes propagate to all calculations across all phases.

### Custom Channels

All channel fields (name, platform, ad type) are free-text. You can model any marketing channel, not just the pre-populated examples.

---

## Technical Details

- **Single-file deployment:** The entire application is one `.html` file (~1,800 lines). No build step, no dependencies, no server.
- **External resources:** Google Fonts (DM Sans) and Phosphor Icons are loaded from CDNs. The tool works offline with fallback system fonts.
- **Browser support:** Any modern browser (Chrome, Firefox, Safari, Edge). No IE support.
- **Print support:** Print stylesheets are included. All phases render when printing.
- **Responsive:** Works on tablet and desktop. Mobile is functional but optimized for wider screens.

---

## FAQ

**Q: Can I use this for non-Goodwall programs?**
A: Yes. All funnel stage names, geographies, channels, and benchmarks are fully editable. Rename stages conceptually to fit your funnel. The math engine is generic.

**Q: How do I embed this in Google Sites?**
A: Host the HTML file (GitHub Pages, Netlify, or any static host), then use Google Sites' **Insert > Embed > By URL** with the hosted URL. Google Sites does not support pasting full HTML pages directly.

**Q: What happens if my allocations don't add up to 100%?**
A: The tool displays a warning but still calculates. Over-allocation (>100%) will project more outcomes than your budget supports. Under-allocation (<100%) means unspent budget.

**Q: Can I have different conversion benchmarks per geography?**
A: The current version uses global benchmarks. Geography-specific variation is modeled through the CPI and Reach Multiplier. For per-geography benchmarks, duplicate the geography with different benchmark assumptions and adjust allocations accordingly.

**Q: Is the data sent anywhere?**
A: No. Everything runs locally in your browser. No data is transmitted to any server. The only network requests are for fonts and icons from public CDNs.
