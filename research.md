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

## Setup: You’re a tech bro launching a revolutionary AI B2B SaaS Crypto Blockchain IoT YC-backed Silicon Valley Startup

Your goal: build a new social media app for college students.  
But, having seen the endless toxicity on platforms like Reddit, X, and Facebook, you want to avoid repeating their mistakes.  
To do that, you need to understand **when** conflict between communities arises, **which types** of conflict are constructive vs harmful, and **why** certain interactions devolve into aggression.

---

## 1. First Steps: *How often does inter-community tension arise?*

* A heavy-tailed distribution confirms that negativity is usually rare.  
* Daily activity plots show that while most crossposts are positive, negative interactions occur regularly—especially between certain pairs of communities.

### Graphs

- **Graph 1 — Proportion of negative crossposts (over time?)**
- **Graph 2 — Distance between community embeddings vs interaction frequency**  
  Shows that similar communities tend to interact more.
- **Graph 3 — Distance between embeddings vs toxicity**  
  Reveals a peak in negativity when communities are moderately far apart—possibly because they represent opposing worldviews (e.g., liberal vs conservative, Chiefs vs Eagles).

**NOTE** I want to add a toxicity vs time or something graph here, like what stefan's notebook included. Not sure exactly what the best way to add that in would be though. 
---

## 2. Interactions Between Specific Communities

Since we know mid-distance communities are more likely to clash, we now zoom into specific pairs of subreddits to illustrate real cases of tension.

* A crosspost flow graph (directed: subreddit → subreddit) reveals how complex and interconnected the ecosystem is.

### Graphs

- **Graph 4 — Subreddit → Subreddit negative-weighted graph**

---

## 3. Clusters: Generalizing Beyond Specific Subreddits

Your future app won’t use the same communities as Reddit, but we can expect similar categories—e.g., city groups, majors, sports fandoms, political affiliations.

Rather than focusing on individual subreddits, we examine **clusters** of related communities to understand broader structural patterns.

### Graphs

- **Graph 5 — Interactive network of clusters**

Using this graph, we can identify the top five most problematic cluster pairs.  
One potential intervention: **reduce or modify cross-cluster exposure** for community pairs that consistently generate toxicity.

---

## 4. Thematic Features: Is All Negativity the Same?

Constructive disagreement is healthy; toxicity is not.  
Research (from the original paper) suggests that even mildly negative crossposts can produce mini-echo chambers in the comment section.  
So simply encouraging “idea exchange” isn’t enough.

* Linguistic profiling reveals strong thematic and emotional signatures across posts.
* Comment-level sentiment (e.g., VADER, LIWC) identifies the degree of hostility in negative crossposts.

### Graphs

- **Graph 6 — Emotional profile of positive vs negative posts**
- **Graph 7 — Stylistic profile of positive vs negative posts**
- **Graph 8 — Emotional + stylistic signatures by community cluster**

We use Graphs 6 and 7 to identify which emotional or stylistic features distinguish constructive disagreements from toxic ones, helping determine which types of interactions should be encouraged vs limited.

---

## 5. Lessons for Your Genius Multi-Billion-Dollar App Idea

* Reduce contact between clusters that consistently generate toxic interactions.  
* Maintain or increase interaction between clusters that tend to have productive, non-toxic debates.  
* Flag or manually monitor particularly problematic communities to stop toxicity before it escalates.

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
