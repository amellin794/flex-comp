# Flex Comp

A single-file tool that lets candidates choose their own cash/equity mix.
Zero dependencies. No build step. Just HTML.

## Quick Start

1. Edit the `CONFIG` object at the top of `index.html`
2. Deploy anywhere (static hosting, S3, Vercel, etc.)
3. Generate personalized links for candidates

## How It Works

- **Admin view** (no URL params): Configure offers with cash salary, preferred share price, fully diluted shares, and equity grant %
- **Candidate view** (with URL params): Interactive slider to trade salary for additional equity, with upside scenarios and vesting timeline

## Customization

All company-specific values live in a single `CONFIG` object at the top of the `<script>` block:

- **Company name & branding** — name, accent color, accent glow
- **Role titles & salary/equity bands** — grouped by department
- **Bonus threshold & rate** — e.g. 10% bonus on salary traded above 20%
- **Vesting terms** — years, cliff, post-termination exercise window
- **Equity plan** — plan name, equity type (ISOs/NSOs)
- **Regional multipliers** — e.g. EU at 0.85x, LATAM at 0.65x
- **Slider range** — min/max/default cash percentage

## Calculation Model

Each candidate offer has a **base cash salary** and an **equity grant** (% of company, valued at the preferred share price).

The slider lets candidates trade cash for additional equity:

```
actual_cash     = base_salary × (slider_pct / 100)
cash_traded     = base_salary - actual_cash
bonus           = max(0, trade_pct - threshold) × base_salary × bonus_rate
total_annual_eq = base_equity_annual + cash_traded + bonus
total_comp      = actual_cash + total_annual_eq
```

Equity vests monthly over the configured vesting period (default: 4 years, no cliff).

## License

MIT
