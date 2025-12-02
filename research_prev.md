---
layout: page
title: Data Analysis Research
subtitle: Exploring patterns and insights through data visualization
permalink: /
full-width: true
ext-js:
  - href: "https://cdn.plot.ly/plotly-2.27.0.min.js"
---

<div class="research-outline" markdown="1">

# Data Story Outline: *A Moderator Under Siege*

## Setup: A mod wakes up to chaos

* Sudden spike in hostile comments and brigading reports.
* A single external subreddit appears repeatedly in the mod logs.
* Goal: understand whether this is a coordinated attack, where it comes from, what patterns it follows, and how to stop it with targeted, temporary interventions.

---

## 1. First signals: “Something is wrong”

* Daily activity plot shows an abnormal burst in inbound crossposts.
* Tone analysis reveals a steep drop in average sentiment for incoming links during the spike.
* Heavy-tail distribution confirms that normally negativity is rare — but today’s event is concentrated and extreme.
* The mod suspects a targeted negative crosslink campaign rather than organic activity.

### Graphs

- **Graph 1 — Global tone over time** (`plot_global_tone()`) shows the sudden negative spike.
- **Graph 2 — Daily inbound crosspost volume** (daily aggregates) highlights the abnormal burst.
- **Graph 3 — Heavy-tail distribution of negative links** (`bar_negative_block_top()`) proves that today's hostility is unusually concentrated.

---

## 2. Where the attack originates

* Crosspost graph (directed subreddit→subreddit) highlights one source community with sudden high negative edge weight.
* Comparison with historical behavior shows this source rarely interacts with the mod’s subreddit.
* The negativity ratio of this source spikes well above its baseline.
* Network structure suggests this is not a multi-community swarm but a single “attack node” dominating.

### Graphs

- **Graph 4 — Subreddit→subreddit negative-weight graph** (`build_graph()`) pinpoints the attacker.
- **Graph 5 — Top negative inbound communities** (`report_plots.bar_negative_block_top`) ranks hostile sources by severity.

---

## 3. How the attackers communicate

* Linguistic profiling of inbound posts shows strong thematic and emotional signatures:
  * Highly negative emotional tone.
  * Stylistic markers typical of “call-to-action” or “mocking” posts.
  * Distinct vocabulary compared to neutral crossposts.
* At the comment level, VADER/LIWC-style sentiment confirms systematic hostility.
* This suggests intentional mobilization, not random disagreement.

### Graphs

- **Graph 6 — Sentiment distribution for attacker vs normal links** compares VADER histograms to show hostility.
- **Graph 7 — Emotional/stylistic linguistic profile comparison** (radar/bar from `linguistic_features.py`) surfaces anger, mockery, and CTA signals.

---

## 4. Why this community targeted us

* Embedding space positioning: the attacking subreddit sits far from the mod’s community cluster.
* Semantic distance (PCA/t-SNE visualization) shows minimal thematic similarity; users rarely overlap.
* Communities near the attacker (in embedding space) share similar linguistic profiles and are also high-negativity hubs.
* The attack is likely “cultural opposition” rather than reaction to a specific post.

### Graphs

- **Graph 8 — Embedding space map** (`similarity.plot_negativity_vs_distance` or custom scatter) places the attacker far from our cluster.
- **Graph 9 — Embedding distance vs negativity** demonstrates how ideological distance correlates with hostile tone.

---

## 5. How bad the situation is

* Block-level Louvain clustering shows the attacker’s whole bloc has elevated negativity.
* Intra-bloc vs inter-bloc stats show the mod’s subreddit is one of the preferred targets of this bloc.
* Temporal windowing reveals the attack escalates quickly, peaks, and decays slowly — a characteristic brigading signature.
* Hostility vs activity plots show high hostility without a matching increase in genuine engagement.

### Graphs

- **Graph 10 — Louvain community structure** (`cluster_louvain()`) distinguishes the hostile bloc from ours.
- **Graph 11 — Block-to-block negativity heatmap** captures the disproportionate targeting.
- **Graph 12 — Hostility vs activity** (`time_communities_utils`) confirms brigading behavior.

---

## 6. How the attack spreads

* Time-window community graphs show negativity diffusing from the attacker to a few “nearby” communities.
* Crossposts from those neighbors replicate the negative framing, amplifying the attack.
* Multiple bursts indicate repeated triggers, possibly from inside the attacker’s subreddit.

### Graphs

- **Graph 13 — Time-sliced network snapshots (T1 → T6)** from `time_communities_utils` visualize the initial spark and spread.
- **Graph 14 — Negativity over time per source** (multi-line windowed chart) shows echo waves and reinforcement bursts.

---

## 7. What the mod can do

* Simulated counterfactual: removing crossposts from the attacker reduces >80% of inbound negativity.
* Short-term intervention: temporarily blocking links from the attacker subreddit.
* Alternative intervention: rate-limiting or requiring manual mod approval for crossposts.
* More precise option: ban only negative-tone crossposts (detected with threshold sentiment).
* Recommendation supported by data: block or throttle the single negative source rather than broad restrictions.

### Graphs

- **Graph 15 — Counterfactual: remove attacker links** quantifies the >80% hostility reduction if edges are cut.
- **Graph 16 — Impact of rate-limiting or crosspost ban** compares simulated policy scenarios (ban, throttle, manual approval).

---

## 8. Aftermath: Did it work?

* Post-intervention metrics show:
  * Inbound crossposts drop sharply.
  * Sentiment normalizes within hours.
  * Community activity stabilizes.
  * No significant spillover retaliation from the attacker’s bloc.
* Long-term monitoring indicates no lasting hostility cycle.

### Graphs

- **Graph 17 — Post-intervention inbound negativity** shows the time series returning to baseline.
- **Graph 18 — Post-intervention sentiment normalization** visualizes VADER tone recovery.
- **Graph 19 — Community activity pre vs post** confirms engagement stabilizes without chilling effects.

---

## 9. Broader lesson for subreddit governance

* The attack is primarily a single-source, culturally distant conflict, not an organic disagreement.
* Targeted, temporary throttling of the hostile node outperforms broad policy shifts.
* Continuous monitoring of embedding distance plus negativity rates helps surface the next siege before it peaks.

### Graphs

- **Graph 20 — Summary dashboard** stitches together the negativity distribution, attacker share, bloc map, and embedding map to reinforce governance takeaways.

**Story placement:** “Takeaways for future moderation and predictive tools.”
</div>

<style>
.research-outline {
  width: min(66.6667vw, 1200px);
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 960px) {
  .research-outline {
    width: 100%;
    padding: 0 1.25rem;
  }
}
</style>
