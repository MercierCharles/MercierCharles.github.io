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
This is very promising for our future app : the normal mode of interaction isn't negative!

The goal now is to understand this 9.7% more.


To do this, we will look at the distribution of the number of negative posts per subreddit:
we rank the subreddits by how many negative posts they send (from most to least) and we plot this distribution on a log-log scale.
![Negative posts per subreddit](/assets/images/negative_subreddit.png)

We recognize a well-known distribution: a heavy-tailed distribution.
This means that a small portion of subreddits concentrate a very large number of negative posts, while the vast majority of subreddits post very few.

That's really encouraging for moderation because we only have to focus on small set of subreddit.

## 2. From individual subreddits to communities

We now know that negativity is concentrated in a small number of subreddits.
But working only at the level of individual subreddits becomes quickly complicated.

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

Now we have the communities, we can see the distribution of the number of negative posts but not per subreddits as before but per communities this time !

![Bar negative block](/assets/images/bar_negative_block.png)

As with the distribution of the number of negative posts per subreddit, a minority of communities are involved in the majority of negative interactions.
Only 43 out of 2086 communities have more than 5 negative posts !

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
This suggests something very interesting for your future app: that moderation should focus on a small core of large communities !

Let's take a closer look at their posts:

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
<iframe 
    src="/assets/data/website_figures/clusters_interaction_network.html"
    style="width:100%; height:70vh; border:none;">
</iframe>

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

## 6. Some good news: metrics over time

In our previous analysis, we determined that the toxicity on Reddit is mainly driven by a few communities.
This is good news as moderating a few toxic communities is much easier than moderating the whole website.

Let's take another angle, that of the evolution over time of the toxic interactions: is it getting better or worse?

This is an interesting question as we want to develop our own social media website, and seeing how reddit's decentralized moderation system works will help us to determine if we use a similar system or not.

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


## 7. Lessons for Your Genius Multi-Billion-Dollar App Idea

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
