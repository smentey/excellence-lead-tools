---
description: "Ready-to-use daily update prompt for Engineering Excellence Leads. Fetches CHG, INC, CAB data from Jira and provides AI tips."
---

# Daily Update Prompt — Engineering Excellence Lead

## Quick Usage

Paste this in Copilot Chat to get your daily dashboard:

### For Team Forge:
```
@Excellence Lead — Give me my daily update for Team Forge.
```

### For Team Connect:
```
@Excellence Lead — Give me my daily update for Team Connect.
```

### For both teams (org-wide view):
```
@Excellence Lead — Give me the full MediVerse daily update for both teams.
```

---

## Setup: Jira Labeling Guide

For the agent to work effectively, your team needs to consistently label Jira tickets. Here's the labeling convention:

### Step 1: Create These Labels in Jira

| Label | When to Apply |
|-------|---------------|
| `excel-forge` | Any ticket owned/tracked by Team Forge |
| `excel-connect` | Any ticket owned/tracked by Team Connect |
| `excel-mediverse` | Spans both teams |
| `excel-chg` | Change request (CHG) tickets |
| `excel-inc` | Incident tickets |
| `excel-cab` | Tickets going through CAB review |
| `excel-release` | Release coordination items |
| `excel-stability` | Stability (STAB) work items |

### Step 2: Always Apply Two Labels

Every ticket gets **one team label + one type label**:

- CHG for Team Forge → `excel-forge` + `excel-chg`
- Incident in Team Connect → `excel-connect` + `excel-inc`
- CAB review for Forge → `excel-forge` + `excel-cab`

### Step 3: Who Labels What?

| Who | Labels |
|-----|--------|
| **Devs** creating CHG tickets | Add `excel-{team}` + `excel-chg` |
| **Excellence Lead** triaging incidents | Add `excel-{team}` + `excel-inc` |
| **Excellence Lead** sending to CAB | Add `excel-cab` |
| **BA/SM** for release items | Add `excel-{team}` + `excel-release` |

---

## Manual JQL Queries (Jira Filters)

If you prefer Jira dashboard filters instead of the agent:

### Team Forge Dashboard Filters

```
-- New CHGs needing approval (Forge)
labels = excel-forge AND labels = excel-chg AND status in ("Awaiting Approval", "New", "Open") AND created >= -1d

-- Incidents last 24h (Forge)
labels = excel-forge AND labels = excel-inc AND created >= -1d

-- Approved CHGs deploying today (Forge)
labels = excel-forge AND labels = excel-chg AND status = "Approved" AND updated >= startOfDay()

-- CAB in review (Forge)
labels = excel-forge AND labels = excel-cab AND status in ("In Review", "CAB Review", "Under Review")
```

### Team Connect Dashboard Filters

```
-- New CHGs needing approval (Connect)
labels = excel-connect AND labels = excel-chg AND status in ("Awaiting Approval", "New", "Open") AND created >= -1d

-- Incidents last 24h (Connect)
labels = excel-connect AND labels = excel-inc AND created >= -1d

-- Approved CHGs deploying today (Connect)
labels = excel-connect AND labels = excel-chg AND status = "Approved" AND updated >= startOfDay()

-- CAB in review (Connect)
labels = excel-connect AND labels = excel-cab AND status in ("In Review", "CAB Review", "Under Review")
```

### Full MediVerse View

```
-- All Excellence Lead tracked items
labels in (excel-forge, excel-connect, excel-mediverse) AND created >= -1d ORDER BY labels, priority DESC
```

---

## Jira Dashboard Setup (Optional)

You can also create a **Jira Dashboard** with saved filters:

1. Go to Jira → Filters → Create Filter
2. Paste the JQL from above
3. Save as "Forge Daily CHGs", "Connect Daily INCs", etc.
4. Go to Dashboards → Create Dashboard
5. Add filter result gadgets for each saved filter

This gives you a browser-based dashboard alongside the agent.
