---
layout: page
title: Data Analysis Research
subtitle: Exploring patterns and insights through data visualization
permalink: /
full-width: true
mathjax: true
ext-js:
  - href: "https://cdn.plot.ly/plotly-2.27.0.min.js"
---

<div class="research-outline" markdown="1">

# Data Story Outline: *Mapping Cross-Subreddit Conflict on Reddit*

## Setup: You’re a tech bro launching a revolutionary AI B2B SaaS Crypto Blockchain IoT YC-backed Silicon Valley Startup

You’ve just raised $3M pre-seed to build a new social app for college students.

There’s just one problem.

Platforms like Reddit, X, and Facebook, despite being rich sources of information and community interaction, all ended up with pockets of extreme hostility, community clashes, and drama.

Before you repeat their mistakes, you need to understand:

- When conflict between communities arises?

- Which types of conflict are constructive vs harmful?

- Why some interactions devolve into hostility while others don’t?

- How can we prevent these same pitfalls in our own social media service?

To answer these questions, you dig into crosspost data from Reddit—one of the most complex ecosystems of online communities.

---

## 1.*How hostile are subreddit interactions, really?*

We begin with a global picture of tone across posts.

![Overall tone](/assets/images/global_tone.png)

Surprisingly, we notice something that is rather encouraging:

**Negativey is the exception, not the norm**

The majority of posts are either positive (90.3%), and only 9.7% are negative.


However, exceptions do matter. Even a relatively small group of negative posts tend to have a large impact on the general athmosphere of social media. Our goal therefore is to understand this 9.7% more.


To do this, we will look at the distribution of the number of negative posts per subreddit:
we rank the subreddits by how many negative posts they send (from most to least) and we plot this distribution on a log-log scale.
![Negative posts per subreddit](/assets/images/negative_subreddit.png)

We recognize a well-known distribution: a heavy-tailed distribution.
This means that a small portion of subreddits contribute to a very large number of negative posts, while the vast majority of subreddits post very few.

Furthermore, by visualizing the number of negative posts per community, we can notice this more concretely. Only 43 out of 2086 communities have more than 5 negative posts!

![Bar negative block](/assets/images/bar_negative_block.png)

For moderation, this is encouraging! 

If a small cluster is responsible for most negative interactions, targeted interventions could be extremely effective. Even minimal moderation has the potential to have a strong impact on ensuring that our new app doesn't fall into the same patterns of toxicity as Reddit.

## 2. From individual subreddits to communities

We now know that negativity is concentrated in a small number of subreddits.

But working only at the level of individual subreddits becomes quickly complicated. Reddit has tens of thousands of subreddit, and looking at these individual subreddits one by one would take months. Furthermore, we're looking for general trends we can learn from. We don't care how a specific subreddit acts, but we do care how they tend to act as a whole.

So what can we do?

We can cluster them! We will group them into communities. There are several methods for doing this, as we'll see, but for now we'll focus on the Louvain method.


We first construct a positive graph (G+) where:
- each node represents a **subreddit**;
- an edge connects two subreddits when there is at least one positive post between them, its weight is the number of positive posts

On this graph (G+), we apply the **Louvain** algorithm to detect groups of subreddits that interact positively with each other.
We found **2086 communities** (blocks of subreddits), with a modularity of approximately **0.55** which indicates that the positive links are well clustered into communities.

### Why work on the graph (G+)?
You might ask why focus on the G+ graph and not on all the positive and negative interactions.
The reason is simple :

- A **positive link** between two subreddits represents the **affinity** between them (same theme, communities that appreciate each other)
- A **negative link**, on the other hand, is more likely to represents a **conflict** between two groups (mockery, attacks, raids)

If we were to use the full graph (with both positive and negative links) to cluster, we would be mixing these two types of relationships and risk grouping subreddits that both like and attack each other into the same "community."

However, what we want to see are the conflicts between communities.
By focusing only on (G+), we amplify the network's affinity structure and then we can analyse how negative links circulate between these blocks to understand where the negativity lies.


It is still a bit abstract, though. To better understand how these communities relate to each other, we now visualize the **community network**:

<div style="text-align: center; margin: 1rem 0;">
  <iframe
    src="/assets/images/network_graph.html"
    width="100%"
    height="500"
    style="border: none;"
  ></iframe>
</div>


It's much more visual! But how do we understand this *network graph*?

Each node represents a community identified by Louvain:

- the color represents its **negativity rate** : $negative\_rate(C) = \dfrac{neg\_out(C)}{total\_out(C)}$ (when $total\_out(C) > 0$).
- each edge represents a **negative link** sent from one community to another
- the size of the node represents the **number of subreddits** in the community.

We observe two main things:

- **A highly connected core**: the largest communities are located there and concentrate most of the negativity : they exchange many negative links with each other and around them, many small communities attack these large communities. These large communities also target certain small communities.
- **Many small communities on the periphery**: they have few or no negative links and don't participate in the negative interactions of the core.

We can conclude that only these large online communities concentrate the majority of the negativity.
This data supports our earlier observation about our moderation strategy: We should focus on a small core of large communities!

So now, let's zoom into this core set of communities: 


## 3. Mapping interactions between high-use communities

Now that we've identified the communities consisting of our 'core' interactions, let's pay attention to these higher-level clusters (e.g., politics, hobbies, geography, lifestyle). In the context of our app, we likely will not have any special communities that map to subreddits. For example, we may not have a community that corresponds to r/nfl or r/nba, but it is very likely that we will have groups of users that create sports communities. So by creating and understanding the interactions between these active high-level clusters, we can understand structural causes of conflict that appear regardless of specific subreddit identities.

### Graphs

- **Graph 5 — Interactive network of clusters**
<iframe 
    src="/assets/data/website_figures/clusters_interaction_network.html"
    style="width:100%; height:70vh; border:none;">
</iframe>

#### Cluster-level drill-down

Pick a cluster to inspect its interaction network, profile, and radar view. The three panels below switch automatically when you change the cluster number.

<div id="cluster-details" class="cluster-details">
  <label for="cluster-select" class="cluster-select-label">
    Select a cluster:
  </label>
  <select id="cluster-select" class="cluster-select">
    <option value="0">Cluster 0</option>
    <option value="1">Cluster 1</option>
    <option value="2">Cluster 2</option>
    <option value="3">Cluster 3</option>
    <option value="4">Cluster 4</option>
    <option value="5">Cluster 5</option>
    <option value="6">Cluster 6</option>
    <option value="7">Cluster 7</option>
    <option value="8">Cluster 8</option>
    <option value="9">Cluster 9</option>
    <option value="10">Cluster 10</option>
    <option value="11">Cluster 11</option>
    <option value="12">Cluster 12</option>
    <option value="13">Cluster 13</option>
    <option value="14">Cluster 14</option>
    <option value="15">Cluster 15</option>
    <option value="16">Cluster 16</option>
    <option value="17">Cluster 17</option>
    <option value="18">Cluster 18</option>
    <option value="19">Cluster 19</option>
  </select>

  <div class="cluster-panels">
    <div class="cluster-panel">
      <div class="cluster-panel-title">Interaction network</div>
      <iframe
        id="cluster-network"
        src="/assets/data/website_figures/clusters_details/cluster_0_network.html"
        loading="lazy"
        style="width:100%; height:60vh; border:none;"
      ></iframe>
    </div>
    <div class="cluster-panel">
      <div class="cluster-panel-title">Linguistic profile</div>
      <iframe
        id="cluster-profile"
        src="/assets/data/website_figures/clusters_details/cluster_0_profile.html"
        loading="lazy"
        style="width:100%; height:60vh; border:none;"
      ></iframe>
    </div>
    <div class="cluster-panel">
      <div class="cluster-panel-title">Thematic radar</div>
      <iframe
        id="cluster-radar"
        src="/assets/data/website_figures/clusters_details/cluster_0_radar.html"
        loading="lazy"
        style="width:100%; height:60vh; border:none;"
      ></iframe>
    </div>
  </div>
</div>

<script>
(function() {
  const select = document.getElementById("cluster-select");
  const frames = {
    network: document.getElementById("cluster-network"),
    profile: document.getElementById("cluster-profile"),
    radar: document.getElementById("cluster-radar"),
  };

  function updateCluster(clusterId) {
    const base =
      "/assets/data/website_figures/clusters_details/cluster_" + clusterId + "_";
    frames.network.src = base + "network.html";
    frames.profile.src = base + "profile.html";
    frames.radar.src = base + "radar.html";
  }

  select.addEventListener("change", function(e) {
    updateCluster(e.target.value);
  });

  updateCluster(select.value);
})();
</script>

From this, we identify the top five conflict-heavy cluster pairs—the types of communities that most often clash:

1. (Personal advice ⟺ Politics, Ideology, and Conspiracies)

2. (Core Gaming ⟺ Technology and Programming)

3. (Personal advice ⟺ Reddit Meta and Drama)

4. (News, Politics, and World Regions ⟺ Politics, Ideology, and Conspiracies)

5. (Memes and Entertainment ⟺ Skepticism and Bad-X Critiques)

Now that we have a way to identify which clusters are most likely to come into conflict, how can we act on it? One approach is to adapt our recommendation algorithm. In particular, we can reduce the visibility of posts from clusters that a user’s home cluster tends to react negatively to, ensuring that users are less frequently exposed to communities with which they historically clash.

In effect, this serves to limit cross-cluster exposure for pairs that produce consistently toxic interactions. There is one signficiant downside to this however - the creation of echo chambers. It's known that when users are surrounded by those who share their own views, this creates 'echo chambers', or communities where extreme views tend to be amplified without being tempered by conflicting opinions. This concern leads us to our next section.

---

## 4. Thematic Features: Is All Negativity the Same?


We know that constructive disagreement is healthy. It avoids the creation of these so called echo chambers. On the other hand, toxic arguments are **not** healthy.  

Research (from the original paper) suggests that even mildly negative crossposts can produce mini-echo chambers in the comment section. So unless we encourage the right type of cross community interactions, there's a strong chance we're only reinforcing the creation of these mini-echo chambers. 


Lucky for us, negativity is not monolithic. We have several different types of negative comments such as:

- Sarcastic but constructive

- Critical but thoughtful

- Outright hostile

- Coordinated attacks

Using linguistic profiling (sentiment models, LIWC-style categories), we can look at the average textual features in each cluster's negative posts. Our aim is to identify which clusters express negativety as critical, constructive arguments, and which clusters express it as hostility and personal attacks.


### Graphs

- **Graph 6 — Emotional profile of positive vs negative posts**
![Negative posts per subreddit](/assets/data/images/emotional_profile_by_cluster.png)

- **Graph 7 — Stylistic profile of positive vs negative posts**
![Negative posts per subreddit](/assets/data/images/stylistic_profile_by_cluster.png)

<iframe 
    src="/assets/images/stylistic_profile_by_cluster.png"
    style="width:100%; height:70vh; border:none;">
</iframe>

- **Graph 8 — Emotional + stylistic signatures by community cluster**

From these, two clusters stand out as especially prone to toxic interactions:

Cluster 7 — “Skepticism and Bad-X Critiques”
Characterized by high anger, swearing, and hostile language

Cluster 1 — “Reddit Meta and Drama”
Exhibits similar patterns, with high caps usage (rant-style posts) and strong emotional volatility

These clusters aren’t just negative—they have recognizably toxic linguistic signatures. On the other hand, a few clusters stand on the opposite side of the spectrum:

Cluster 2 — "Personal Idea and Mental Health"
Low Swearing, but high anxiety and sadness

Cluster 12 — "Cities, Career, and Everyday Life 

What does this tell us in terms of our new app?

When adjusting our algorithm we want to ensure that users active in clusters such as 12 and 2 tend to see other communities more often since they are more likely to exhibit negativey in a healthier way.

On the other hand, users from Clusters 7 and 1 are more likely to create comments that are angrier and more hostile. So like we mentioned in the previous section, it would be useful to prevent users from these communities from being shown posts from clusters they are likely to interact negatively with Additionally, targeting these clusters allows us to deploy our moderation efforts- a limited resource- where they will have the greatest impact.

## 5. The Solution: The Moderation Matrix

We have identified who fights (the clusters) and how they fight (the linguistic profile). Now, the final question for our startup is: **How do we fix it without going bankrupt?**

Hiring human moderators is expensive, while AI moderation is cheap but struggles with nuance. To solve this, we developed the **Moderation Matrix (Graph 9)** to prioritize resources based on two factors: **Scale** (Interaction Volume) and **Risk** (Toxicity Ratio).

### Graph 9 — The Moderation Matrix

<iframe 
    src="/assets/data/website_figures/graph_9_moderation_matrix.html"
    style="width:100%; height:70vh; border:none;">
</iframe>

Graph 9 confirms that toxicity follows a strict Pareto Principle (80/20 rule). A tiny fraction of communities creates the vast majority of our problems. By plotting our 20 communities on this Log-Log scale, distinct strategies emerge for different quadrants:

* **The "Kill Zone" (Top Right)**
    * **Characteristics:** High Volume, High Toxicity.
    * **Example:** **Politics, Ideologies, and Conspiracies (Cluster 6)**. This cluster is massive and consistently hostile.
    * **Strategy:** **Manual Moderation Required.** This is where we burn our budget. These communities are too large to ignore and too nuanced for AI to catch every dog-whistle. Human intervention is mandatory here to prevent site-wide contamination.

* **Niche Hate (Top Left)**
    * **Characteristics:** Low Volume, High Toxicity.
    * **Example:** **Meta-Politics and Watchdog Communities (Cluster 11)**.
    * **Strategy:** **Automated Flagging.** These are small, isolated pockets of negativity. Because they don't drive massive traffic, we can aggressively use strict AI keyword filters. If we accidentally ban a false positive here, the impact on the platform's overall growth is minimal compared to the "Kill Zone".

* **Healthy Viral (Bottom Right)**
    * **Characteristics:** Massive Volume, Low Toxicity.
    * **Example:** **Memes and Entertainment (Cluster 15)**.
    * **Strategy:** **Self-Regulation.** These communities are the "Golden Geese". They are huge and active but remain civil. We should do nothing here; heavy-handed moderation would only stifle their growth. Let the community downvote buttons do the work.

**The Startup Takeaway:** Don't try to moderate the whole internet. Ignore the bottom-right, automate the top-left, and send your human team into the top-right Kill Zone.

---

## 6. Timing is Everything: The "Viral Outrage"

Finally, we must understand *when* to deploy these resources. Is toxicity a constant background hum, or does it strike like lightning?

We analyzed the volume of interactions over time, stacking positive exchanges against toxic conflict.

### Graph 1b — The "Viral Outrage" Timeline

<iframe 
    src="/assets/data/website_figures/graph_1b_viral_outrage.html"
    style="width:100%; height:70vh; border:none;">
</iframe>

The data refutes the idea that "internet trolls are always on". Conflict is not a flat line; it is bursty and follows a pattern of **Volatility Clustering**.

* **The Baseline:** For most of the timeline (green area), the platform is overwhelmingly positive.
* **The Spikes:** Look at the "Peak Volatility" on the far right. We see sudden, sharp expansions in the red area (toxic conflict).

**What causes these bursts?** These spikes usually correlate with external real-world events (elections, scandals, viral news). When these events hit, the "Kill Zone" communities identified above flare up simultaneously.

**The Operational Lesson:** We don't need a massive standing army of moderators 24/7. Instead, we need **Surge Capacity**. Our system needs to detect the initial slope of a "red spike" (as seen in late 2017) and dynamically scale server costs only when the alarm sounds.

---

## 7. The Algorithm: From Reaction to Prediction

Descriptive graphs are useful, but to build a scalable platform, we need predictive metrics. We don't just want to watch the house burn; we want to catch the spark.

To do this, we treat toxicity not as "bad behavior," but as a virus.

#### The "Toxicity $R_0$" (Viral Coefficient)

In epidemiology, $R_0$ represents the reproduction number of a virus—how many people one infected person will infect. We applied this same logic to our community clusters.

We define the **Viral Toxicity Coefficient ($R_0$)** as:

$$R_0 = \frac{\text{Rate of new toxic replies}}{\text{Rate of moderation and deletion}}$$

*(Note: The formula logic is inverted from standard removal rates to reflect viral growth potential, or strictly as defined in your heuristic)*

This formula gives us a binary decision matrix for our automated systems:

* **If $R_0 < 1$ (Decay):** The conflict is dying out naturally. Even if the volume is high (like in **Memes and Entertainment (Cluster 15)**), intervention is unnecessary. The community's immune system is working.
* **If $R_0 > 1$ (Growth):** The toxicity is self-sustaining and expanding. This triggers an immediate alert to the "Kill Zone" moderators.

#### Mapping the Contagion Vectors

Finally, we asked: **How does the infection escape the Kill Zone?**

If the toxic **Politics, Ideologies, and Conspiracies (Cluster 6)** was isolated, we could simply ban it. However, our network analysis reveals a more dangerous structure: **Bridge Communities**.

We found that mid-sized clusters—specifically **Reddit Meta and Drama (Cluster 1)**—often act as "Vectors". They do not originate the hate, but they import memes and language from the Kill Zone and sanitize them for the mainstream.

**The Strategy:** To stop the spread, we don't just police the source (Red nodes) or protect the victims (Green nodes). **We cut the bridges.** By strictly moderating crossposts passing through "Vector" communities, we break the chain of transmission ($R_0$) before it reaches the healthy viral clusters.

## 8. Some good news: metrics over time

In our previous analysis, we determined that the toxicity on Reddit is mainly driven by a few communities.
This is good news as moderating a few toxic communities is much easier than moderating the whole website.

Let's take another angle, that of the evolution over time of the toxic interactions: is it getting better or worse?

Answering this question would allow us to understand whether we need to take more drastic steps to address the possible spread of toxicity in our app.


Since we now are a veteran of ADA's methodology, let's first take a look at how the network evolves over time before making any hasty conclusions!

Below are 4 time graphs with statistics over a moving window of 1 month, made by our very smart colleague. Sadly, he forgot to annotate these "trivial graphs". Let's not panic and put on our detective hat to understand these:

![community_metrics_over_time](/assets/images/community_metrics_over_time.png)

On the top left and top right graphs, we can see that the number of edges & nodes increases almost linearly, which is slightly surprising since reddit had an explosive growth in that timeframe, but it's a particularity of the way reddit has communities.

Indeed, while the number of users grew exponentially over that timeframe [TODO CITE], one can explain this linear growth by simple graph theory: '[preferential attachment](https://en.wikipedia.org/wiki/Preferential_attachment)', a fancy word for "the rich get richer". In our case here, new users join existing communities instead of creating new ones, meaning that those communities grow larger. But we'll get back to that last part.

Now let's try to understand the ones at the bottom, starting with
- The bottom left: the degree of a window over time. The degree is the number of connections(edges) each node has to other nodes. The higher, the more connected the graph is. We can see that over time this number fluctuates quite a bit, but on average it increases over the timeframe: Reddit becomes more interconnected, more dialog! This is good news, we want to emulate the same behavior in our social media.
- The bottom right: You remember you're a detective that took the [internet analytics class](https://edu.epfl.ch/coursebook/en/internet-analytics-COM-308) and vaguely remember that the modularity, in a nutshell (see below for complete explanation) is the expected number of edges between two nodes. This is a measure of how much the graph is "community-ified". A score of 0.6+ is a high score for such a graph, meaning that reddit is quite well partitioned in communities. This is good as Reddit managed to group similar people together, but the flipside is that Reddit also could potentially lead to "echo chambers". This is something we need to watch out for in our new social media.

[TODO explain the modularity]

Now, let's take a look at the proportion of positive posts vs negatives over time. Ah, our colleague made just the perfect graph! Let's take a closer look:
![a](/assets/images/positives_vs_negatives_time_dual_axis.png)

Well that's not exactly good news... It seems that the number of positive interactions grows the same as the negatives. This means that the reddit way of moderating is keeping the status quo, not improving it.

BUT WAIT, let's not be too hasty, indeed we are now a seasoned ADA enthusiast. Let's make sure we understand the graph before concluding that Reddit moderation is bad, even if it seems likely.

Hmmmm, the timescale looks the same as the other graph, the labels make sense, but there aha! The scales are different! Our sneaky colleague put both numbers on 2 different axies, and indeed the proportional growth of the positive and negative interactions is about the same.

But, let's plot them on the same scale:
![b](/assets/images/positives_vs_negatives_time_single_axis.png)

Aha! The negative interactions pale in comparison to the positive ones, so actually this is excellent news! This means

Let's now make a graph of our own to find out the few negative interactions are coming from. We want to find out if it's general negativity or if it's particular communities:
![c](/assets/images/hostility_vs_activity.png)

[TODO reformulate or remove since it's basically the same graph as in the introduction]

We can see that most communities are in the lower half, and that there are a few clusters in the upper parts of the graph. This is excellent news, as this means that we can focus our moderating efforts on those "toxicity prone" communities and thus curb the general toxicity on Reddit!


## 9. Final Lessons

Your analysis reveals three major insights for your hypothetical startup:

Negativity is rare—but highly concentrate: focused moderation can have disproportionate impact.

*A small core of communities drives most conflicts*: Community-level tools (not just individual-level) matter.

*Not all negativity is harmful:* Emotional and stylistic features help distinguish critique from toxicity. As a result, we should focus on communities that frequency display these negative characteristics

---
</div>

<style>
.research-outline {
  width: min(66.6667vw, 1200px);
  margin: 0 auto;
  padding: 0 2rem;
}

.cluster-details {
  margin: 1.5rem 0 2rem;
}

.cluster-select-label {
  font-weight: 600;
  margin-right: 0.5rem;
}

.cluster-select {
  padding: 0.35rem 0.65rem;
  border-radius: 6px;
  border: 1px solid #d0d7de;
  background: #fff;
}

.cluster-panels {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1rem;
}

.cluster-panel {
  background: #f8f9fa;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 0.75rem;
}

.cluster-panel-title {
  font-weight: 600;
  margin-bottom: 0.5rem;
}

@media (max-width: 960px) {
  .research-outline {
    width: 100%;
    padding: 0 1.25rem;
  }
}
</style>
