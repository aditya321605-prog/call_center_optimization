# Call Center Staffing: A Queueing Simulation

Discrete-event simulation of a call center as an **M/M/s queue**, used to decide how many agents to schedule. Arrival rate is 20 calls/hour, each agent serves 5 calls/hour, and the service goal is that 95% of callers wait no more than 5 minutes.

## What it covers

- Simulation engine (Poisson arrivals, exponential service, FCFS, optional abandonment and agent breaks)
- Validation against the exact Erlang C formulas (simulation matches theory within sampling error)
- Staffing levels vs. the 5-minute wait target
- Time-varying demand (30 / 20 / 40 calls per hour across the shift)
- Caller abandonment with a 5-minute patience
- Agent breaks, compared using identical simulated calls
- Cost optimisation (agent wages vs. cost of waiting)
- 30-day variability of wait times

## Key results (seed 1, 200 simulated shifts per scenario)

- Offered load is 4 agents' worth of work, so **4 or fewer agents never stabilise**; waits grow all shift.
- **7 agents** are the minimum that meet the 95th-percentile target (4.3 min); 6 agents give 10.7 min.
- Under time-varying demand a constant crew needs **10 agents** to meet the target, which is why shift-level scheduling matters.
- The cost-minimising crew is **6 agents**, but it misses the target on most simulated days (12 of 30 met it), so the target costs extra staffing.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook call_center_simulation.ipynb
```

Runs in about 15 seconds. Edit `LAMBDA`, `MU`, `WAIT_TARGET_MIN` and the cost parameters in the notebook to model a different call center.

## Notes

- Each shift starts with an empty queue, so short-shift waits are slightly below steady-state values.
- Arrivals are Poisson and service times exponential; real call durations are usually heavier-tailed.
