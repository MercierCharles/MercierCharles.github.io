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

## 1. First Steps: *How hostile are the interactions between subreddits?*

First of all, let's look at the proportion of negative posts across the subreddits.

![Overall tone](/assets/images/global_tone.png)

We notice something very interesting and encouraging:
the majority of posts are either positive or neutral (90.3%), and only 9.7% are negative.
This is very promising for our future app, as it means that the normal mode of interaction isn't negative!

The goal now is to understand this 9.7% more.


To do this, we will look at the distribution of the number of negative posts per subreddit:
we rank the subreddits by how many negative posts they send (from most to least) and we plot this distribution on a log-log scale.
![Negative posts per subreddit](/assets/images/negative_subreddit.png)

We recognize a well-known distribution: a heavy-tailed distribution.
This means that a small portion of subreddits concentrate a very large number of negative posts, while the vast majority of subreddits post very few.

That's really encouraging for moderation because we only have to focus on small subreddit.

## 2. From individual subreddits to communities


Now that we know negativity is concentrated in a small number of subreddits, we can get a more structural view of the network.



Rather than looking at subreddits one by one, we group them into **communities** (or “blocks”) of related subreddits.


We first construct a positive graph (G+) where:
- each node represents a **subreddit**;
- an edge connects two subreddits when they send each other many positive posts.

On this graph (G+), we apply the **Louvain** algorithm to detect groups of subreddits that interact positively with each other.
We found **2,086 communities** (blocks of subreddits), with a modularity of approximately **0.55** which indicates that the positive links are well clustered into communities.


What is louvain ?

### Why work on the graph (G+)?
You might ask why focus on the G+ graph and not on all the positive and negative interactions.
The reason is simple :

- A **positive link** between two subreddits represents the **affinity** between them (same theme, communities that appreciate each other)
- A **negative link**, on the other hand, is more likely to represents a **conflict** between two groups (mockery, attacks, raids)

If we were to use the full graph (with both positive and negative links) to cluster, we would be mixing these two types of relationships and risk grouping subreddits that both like and attack each other into the same "community."

However, what we want to see are the conflicts between communities.
By focusing only on (G+), we amplify the network's affinity structure and then we can analyse how negative links circulate between these blocks to understand where the negativity lies.

Now we have the communities, we can see the distribution of the number of negative posts but not per subreddits as before but per communities this time !

![Bar negative block](/assets/images/bar_negative_block.png)

As with the distribution of the number of negative posts per subreddit, a minority of communities are involved in the majority of negative interactions.
Only 43 out of 2082 communities have more than 5 negative posts !

It is still a bit abstract, though. To better understand how these communities relate to each other, we now visualize the **community network**:

<div style="text-align: center; margin: 1rem 0;">
  <iframe
    src="/assets/images/network_graph.html"
    width="100%"
    height="500"
    style="border: none;"
  ></iframe>
</div>


That's more parlant !

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

Linguistic profiling reveals strong thematic and emotional signatures across posts.
Comment-level sentiment (e.g., VADER, LIWC) identifies the degree of hostility in negative crossposts.

We should use these two to figure out what pairs of subreddit/cluster interactions are toxic and what aren't.
### Graphs

- **Graph 6 — Emotional profile of positive vs negative posts**
- **Graph 7 — Stylistic profile of positive vs negative posts**
- **Graph 8 — Emotional + stylistic signatures by community cluster**

We use Graphs 6 and 7 to identify which emotional or stylistic features distinguish constructive disagreements from toxic ones, helping determine which types of interactions should be encouraged vs limited. Ideally we end up with a couple of subreddits that perhaps need more moderation.

## 5. Manual moderation

Leading in from the previous point, let us take the top 1 or two clusters in terms of negativety and check how negative they are. We can state that certain clusters, due to the amount of hostility in crossposts, require manual moderation. We aim to figure out what those clusters are. 

(Note, the clusters we pick can be relatively arbritrary, we can just state that due to a certain shared feature such as a high emotional characteristic or volume of crossposts they need more moderation. The feature just need to be quantitative)

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
