# Traffic light control using Markov Decision Processes (MDPs)

> Adaptive traffic-signal control with Markov Decision Processes using real congestion patterns from Casablanca. The simulator learns an optimal policy (value/policy iteration) and benchmarks it against a random baseline over a full simulated week.

---

## overview

Urban traffic is stochastic and context-dependent (time of day, weekday vs weekend, weather, special events). Fixed-time signals struggle with these dynamics.  
This project formulates **single-intersection control** as an **MDP** and learns **optimal signal policies** that react to changing conditions. Real congestion levels are inferred from **hourly travel times over 440 city trajectories** (Casablanca), which drive the arrival rates used in simulation.

**headline results (from the accompanying report):**
- **~23% reduction** in cumulative CO₂-proxy emissions under the learned policy vs a random baseline.
- Slight trade-off on average queue length (≈4.57 → 4.62), reflecting reward design priorities (environmental cost vs throughput).
- Policies remain robust under **rain** and **event** surges.

---

## key contributions

- **MDP environment** with rich state: queues (NS/EW), time of day, weekday/weekend, weather, event flags/types, nearby landmark context.
- **Action set** reflecting real phases: `GREEN_NS_30`, `GREEN_EW_30`, `GREEN_NS_60`, `GREEN_EW_60`, `ALL_RED_10`.
- **Reward** penalizing idle time, queue length, and a CO₂-proxy (idle × duration), with γ = 0.95.
- **Learning** via **value iteration** (and **policy iteration**) + comparison to a random policy over **1,680 steps** (7 days × 24 h × 10 steps/h).
- **Data-driven arrivals**: Poisson λ depends on hour/day, rain, and event activity, calibrated from Casablanca travel-time profiles.

