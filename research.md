---
layout: page
title: Data Analysis Research
subtitle: Exploring patterns and insights through data visualization
permalink: /
full-width: true
ext-js:
  - href: "https://cdn.plot.ly/plotly-2.27.0.min.js"
---

## Overview

This page presents my ongoing data analysis research, where I explore various datasets to uncover meaningful patterns, relationships, and insights. Through statistical analysis and visualization, I aim to understand complex phenomena and communicate findings effectively.

## Research Methodology

My approach combines rigorous statistical methods with intuitive visualizations to make data-driven insights accessible. I employ various techniques including time series analysis, distribution modeling, correlation studies, and comparative assessments.

## Key Findings

### Time Series Analysis

Understanding temporal patterns is crucial for identifying trends and forecasting future behavior. The following interactive visualization demonstrates a time series analysis of our dataset. You can zoom, pan, and hover over data points to explore the details:

<div id="time-series-plot" style="width:100%; height:500px;"></div>

*Figure 1: Interactive time series analysis showing data trends over time. The red dashed line represents the underlying trend, while the blue line shows the actual observed data with natural variation. Use the toolbar to zoom, pan, or download the plot.*

### Distribution Analysis

Examining the distribution of data points helps us understand the underlying structure and identify outliers or anomalies. Hover over the bars to see exact frequencies:

<div id="distribution-plot" style="width:100%; height:500px;"></div>

*Figure 2: Interactive histogram showing the frequency distribution of values. The red dashed line indicates the mean value, providing a central tendency measure.*

### Correlation Analysis

Understanding relationships between variables is essential for building predictive models and identifying key factors. Hover over the heatmap cells to see exact correlation values:

<div id="correlation-plot" style="width:100%; height:500px;"></div>

*Figure 3: Interactive correlation matrix heatmap showing the strength and direction of relationships between different variables. Values range from -1 (perfect negative correlation) to +1 (perfect positive correlation).*

### Comparative Analysis

Comparing different groups or categories reveals important differences and similarities. Click on the legend to toggle groups on and off:

<div id="comparative-plot" style="width:100%; height:500px;"></div>

*Figure 4: Interactive comparative bar chart showing values across different categories for two distinct groups. This visualization helps identify patterns and differences between groups.*

## Conclusions

Through comprehensive data analysis and visualization, we can extract meaningful insights that inform decision-making processes. The combination of statistical rigor and clear visual communication enables both technical and non-technical audiences to understand complex data relationships.

## Future Work

Future research directions include:
- Advanced machine learning models for prediction
- Multivariate analysis techniques
- Real-time data streaming analysis
- Integration of additional data sources

## Community Insights Gallery

Beyond the summary charts above, the research stack produces a suite of ready-to-share dashboards exported to standalone Plotly HTML files under `assets/data/website_figures`. The highlights below are embedded directly so you can interact with the same figures that appear in reports and presentations.

<div class="figure-grid">
  <div class="figure-card">
    <h4>Overall Tone Trajectory</h4>
    <p class="figure-caption">Weekly sentiment pulse combining VADER and LIWC affective markers.</p>
    <iframe
      title="Overall tone trajectory"
      loading="lazy"
      src="{{ '/assets/data/website_figures/overall_tone.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Community Stats Overview</h4>
    <p class="figure-caption">Top-level KPIs for volume, engagement, and moderation signals.</p>
    <iframe
      title="Community stats overview"
      loading="lazy"
      src="{{ '/assets/data/website_figures/community_stats_overview.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Hostility vs Activity</h4>
    <p class="figure-caption">Scatter plot contrasting toxic rates with posting intensity for each cluster.</p>
    <iframe
      title="Hostility vs activity"
      loading="lazy"
      src="{{ '/assets/data/website_figures/hostility_vs_activity.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Community Sizes Over Time</h4>
    <p class="figure-caption">Stacked area timeline that reveals how emerging cohorts grow or decay.</p>
    <iframe
      title="Community sizes over time"
      loading="lazy"
      src="{{ '/assets/data/website_figures/community_sizes_over_time.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Cluster Emotional Profiles</h4>
    <p class="figure-caption">Heatmap comparing normalized emotional vectors across discovered clusters.</p>
    <iframe
      title="Cluster emotional profiles heatmap"
      loading="lazy"
      src="{{ '/assets/data/website_figures/cluster_emotional_profiles_heatmap.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Subreddit Embeddings Map</h4>
    <p class="figure-caption">2D projection of subreddit embeddings colored by inferred community.</p>
    <iframe
      title="Subreddit embeddings map"
      loading="lazy"
      src="{{ '/assets/data/website_figures/subreddit_embeddings_map.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Tone Over Time</h4>
    <p class="figure-caption">Temporal evolution of sentiment and emotional markers across the dataset.</p>
    <iframe
      title="Tone over time"
      loading="lazy"
      src="{{ '/assets/data/website_figures/tone_over_time.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Cluster Thematic Radar</h4>
    <p class="figure-caption">Radar chart showing thematic composition across different clusters.</p>
    <iframe
      title="Cluster thematic radar"
      loading="lazy"
      src="{{ '/assets/data/website_figures/cluster_thematic_radar.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Communities vs GCC</h4>
    <p class="figure-caption">Comparison between discovered communities and ground truth GCC classifications.</p>
    <iframe
      title="Communities vs GCC"
      loading="lazy"
      src="{{ '/assets/data/website_figures/communities_vs_gcc.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Community Negative Network</h4>
    <p class="figure-caption">Network visualization showing negative interactions between communities.</p>
    <iframe
      title="Community negative network"
      loading="lazy"
      src="{{ '/assets/data/website_figures/community_negative_network.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Emotional Profile Differences</h4>
    <p class="figure-caption">Visualization highlighting differences in emotional profiles between groups.</p>
    <iframe
      title="Emotional profile differences"
      loading="lazy"
      src="{{ '/assets/data/website_figures/emotional_profile_differences.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Linguistic Profiles Map</h4>
    <p class="figure-caption">Spatial representation of linguistic characteristics across communities.</p>
    <iframe
      title="Linguistic profiles map"
      loading="lazy"
      src="{{ '/assets/data/website_figures/linguistic_profiles_map.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Negative Posts Distribution</h4>
    <p class="figure-caption">Distribution analysis of negative content across different dimensions.</p>
    <iframe
      title="Negative posts distribution"
      loading="lazy"
      src="{{ '/assets/data/website_figures/negative_posts_distribution.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Subreddit Clusters Map</h4>
    <p class="figure-caption">Geographic or embedding-space visualization of subreddit cluster assignments.</p>
    <iframe
      title="Subreddit clusters map"
      loading="lazy"
      src="{{ '/assets/data/website_figures/subreddit_clusters_map.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
  <div class="figure-card">
    <h4>Top Negative Blocks</h4>
    <p class="figure-caption">Identification and visualization of the most problematic content blocks.</p>
    <iframe
      title="Top negative blocks"
      loading="lazy"
      src="{{ '/assets/data/website_figures/top_negative_blocks.html' | relative_url }}"
      style="width:100%; min-height:520px; border:1px solid #e5e5e5; border-radius:8px; background:#fff;">
    </iframe>
  </div>
</div>

---

*Note: The interactive plots above are generated using Plotly. To update the visualizations, modify the `generate_plots.py` script and regenerate the JSON files.*

<script>
// Load and render Plotly plots
document.addEventListener('DOMContentLoaded', function() {
    const plotSources = {
        time: '{{ "/assets/data/research/time_series.json" | relative_url }}',
        distribution: '{{ "/assets/data/research/distribution.json" | relative_url }}',
        correlation: '{{ "/assets/data/research/correlation.json" | relative_url }}',
        comparative: '{{ "/assets/data/research/comparative.json" | relative_url }}'
    };

    // Load Time Series Plot
    fetch(plotSources.time)
        .then(response => response.json())
        .then(data => {
            Plotly.newPlot('time-series-plot', data.data, data.layout, {responsive: true});
        })
        .catch(error => console.error('Error loading time series plot:', error));
    
    // Load Distribution Plot
    fetch(plotSources.distribution)
        .then(response => response.json())
        .then(data => {
            Plotly.newPlot('distribution-plot', data.data, data.layout, {responsive: true});
        })
        .catch(error => console.error('Error loading distribution plot:', error));
    
    // Load Correlation Plot
    fetch(plotSources.correlation)
        .then(response => response.json())
        .then(data => {
            Plotly.newPlot('correlation-plot', data.data, data.layout, {responsive: true});
        })
        .catch(error => console.error('Error loading correlation plot:', error));
    
    // Load Comparative Plot
    fetch(plotSources.comparative)
        .then(response => response.json())
        .then(data => {
            Plotly.newPlot('comparative-plot', data.data, data.layout, {responsive: true});
        })
        .catch(error => console.error('Error loading comparative plot:', error));
});
</script>

<style>
.figure-grid {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-top: 1.5rem;
}

.figure-card {
  width: 100%;
  margin-bottom: 2rem;
}

.figure-card h4 {
  margin-bottom: 0.35rem;
}

.figure-caption {
  font-size: 0.95rem;
  color: #666;
  margin-bottom: 0.75rem;
}

/* Make content area wider but not full width */
main.container-fluid .col {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}
</style>

