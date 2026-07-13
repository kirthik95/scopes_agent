# scopes_agent

Daily bug-bounty scope-discovery + hunting agent. Runs once a day in an isolated Anthropic cloud sandbox (Claude Code routine `Daily Scope Hunter`, cron `0 3 * * *` UTC = 8:30 AM IST).

## What it does
1. **Discover** — pulls new bug-bounty scopes added in the last 24h (ProjectDiscovery Chaos index, BBRadar, HackerOne / Bugcrowd / Intigriti / YesWeHack public directories).
2. **Triage** — reads each program policy. Automation-allowed → full hunt. Forbidden/unclear → discover-only.
3. **Hunt** — non-destructive P1/P2 recon on in-scope, automation-allowed assets (subdomain enum, exposure checks, takeover, CORS/open-redirect). Single safe request per check.
4. **Report** — commits `reports/YYYY-MM-DD.md` here each run.

## Rules (enforced in the agent prompt)
- Authorized, in-scope assets only.
- Non-destructive: no exploitation past a single safe PoC, no DoS, no brute force, no exfiltration.
- Automation only where program policy permits.

## Reports
Dated findings land in [`reports/`](reports/).
