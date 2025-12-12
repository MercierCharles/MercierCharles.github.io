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

![a](/assets/images/emotional_profile_by_cluster.png)
![a](/assets/images/stylistic_profile_by_cluster.png)

From these, two clusters stand out as especially prone to toxic interactions:

Cluster 7 — “Skepticism and Bad-X Critiques”
Characterized by high anger, swearing, and hostile language

Cluster 1 — “Reddit Meta and Drama”
Exhibits similar patterns, with high caps usage (rant-style posts) and strong emotional volatility

These clusters aren’t just negative—they have recognizably toxic linguistic signatures. On the other hand, a few clusters stand on the opposite side of the spectrum:

Cluster —
Cluster — 

 What does this tell us in terms of our new app?

It suggests that manual moderation—a limited resource—should be concentrated on communities resembling clusters 1 and 7. Targeting these clusters allows us to deploy our moderation efforts where they will have the greatest impact.

## 5. Some good news: metrics over time

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


## 5. Final Lessons

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

@media (max-width: 960px) {
  .research-outline {
    width: 100%;
    padding: 0 1.25rem;
  }
}
</style>
