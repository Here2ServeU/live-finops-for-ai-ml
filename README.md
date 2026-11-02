# FinOps for AI-ML Systems · Free Live Sessions

See every dollar, cut the waste not the model, and build budgets that bite.

**Free · Live · 30 minutes · Mondays and Thursdays, 7:30 PM Central** · with Emmanuel N. ([Transformed 2 Succeed](https://transformed2succeed.com))

### [Register free on Zoom](https://us06web.zoom.us/meeting/register/fT235rLjQaihJYrWj2_vjw)

Register once and you're in for every session. Zoom emails you the join link and reminders. Bring your questions: every session ends with live Q&A.

## Watch the recordings

Missed a session or want to watch it again? Recordings are added here after each live session.

| Date | Recording |
|---|---|
| _Coming after the first session_ | |

## Download the slides

**[07_FinOps_for_AI_ML_Systems_Free_Live_Session.pdf](slides/07_FinOps_for_AI_ML_Systems_Free_Live_Session.pdf)** (PDF)

## What you'll learn

1. **See Every Dollar**: Read a month of AI bills: where the money goes, who owns it, what one prediction costs.
2. **Cut the Waste, Not the Model**: Stop idle GPUs, train on spot safely, and cut the LLM bill above a quality floor.
3. **Budgets That Bite**: Forecast every team's month, catch spikes on day one, and gate new spend before it exists.

## Three things to remember

- **You can't cut what you can't see**: Module 1: where, who, per what. Three tags, showback, unit cost.
- **Pay for work, not for waiting**: Module 2: idle GPUs, spot with checkpoints, route and reuse, quality floor.
- **Every dollar: an owner and an alarm**: Module 3: forecast, alert, gate, and a weekly rhythm.

## Try it yourself

Get the hands-on labs here: [finops-for-ai-ml](https://github.com/Here2ServeU/finops-for-ai-ml)

**Module 1 · See Every Dollar**: Give every dollar an owner

```bash
python3 lab/make_data.py
python3 module-1/tag_audit.py; echo "exit $?"
cp module-1/tags.example.json module-1/tags.json
python3 module-1/showback.py
```

**Module 2 · Cut the Waste, Not the Model**: Pay for work, not for waiting

```bash
python3 module-2/idle.py
python3 module-2/spot_sim.py
python3 module-2/llm_router.py
```

**Module 3 · Budgets That Bite**: Forecast, alert, gate

```bash
python3 module-3/forecast.py
python3 module-3/anomaly.py
python3 module-3/cost_gate.py module-3/change-bad.json
python3 -m unittest discover tests
```

## All free live sessions

A different course every session. The rotation repeats every 4 weeks, so if you miss one, it comes back around.

| Week | Day | Course |
|---|---|---|
| Week 1 | Monday | [Linux for AI-ML Systems](https://github.com/Here2ServeU/live-linux-for-ai-ml) |
| Week 1 | Thursday | [Python for AI-ML](https://github.com/Here2ServeU/live-python-for-ai-ml) |
| Week 2 | Monday | [Zero to AI-ML Systems Engineering](https://github.com/Here2ServeU/live-zero-to-ai-ml) |
| Week 2 | Thursday | [DevOps for AI-ML Systems](https://github.com/Here2ServeU/live-devops-for-ai-ml) |
| Week 3 | Monday | [SRE for AI-ML Systems](https://github.com/Here2ServeU/live-sre-for-ai-ml) |
| Week 3 | Thursday | [GPU Optimization for AI-ML Systems](https://github.com/Here2ServeU/live-gpu-optimization-for-ai-ml) |
| Week 4 | Monday | **FinOps for AI-ML Systems** (you are here) |
| Week 4 | Thursday | [AI Agent Operations](https://github.com/Here2ServeU/live-ai-agent-operations) |

## Want the full course?

The membership gives you **all 8 courses, every module and every lab, for $49/month**, plus a live session every month where we build something together.

**[Join at transformed2succeed.com](https://transformed2succeed.com)**
