---
layout: splash
classes:
  - narrow
permalink: /papers/Lifespace/
title: "Causal Models with Tiny Data: The Case of Rural People Living with Dementia"
category: precision-health
description: 'by Ranveer Singh, Saurabh Mathur, Kavimayil P. Komarasamy, Ameet Soni, Cliff Whetung, Wayne Warry, Kristen Jacklin, Melissa Blind, Sriraam Natarajan, In AIME 2026'
author: ['Ranveer Singh','Saurabh Mathur']
excerpt: '<i>Ranveer Singh, Saurabh Mathur, Kavimayil P. Komarasamy, Ameet Soni, Cliff Whetung, Wayne Warry, Kristen Jacklin, Melissa Blind, Sriraam Natarajan</i><br/>UT Dallas &nbsp;&middot;&nbsp; TU Darmstadt &nbsp;&middot;&nbsp; Swarthmore &nbsp;&middot;&nbsp; University of Minnesota Medical School<br/><br/>{::nomarkdown}<a href="https://starling-lab.github.io/assets/pdfs/AIME2026_Lifespace.pdf" class="btn btn--light-outline btn--large"><i class="fas fa-file-pdf"></i> Paper</a> <a href="https://github.com/s-ranveer/AIME_Lifespace" class="btn btn--light-outline btn--large"> <i class="fab fa-github"></i> Code</a>{:/nomarkdown}'
toc: true
header:
  image: /assets/images/project/Lifespace_fig.png
  teaser: /assets/images/project/Lifespace_fig.png
  overlay_color: SteelBlue
---

> Causal modeling for specialized populations like non-urban dementia patients is critical for developing targeted interventions, yet reliable causal models are unavailable. We study several approaches for building causal graphs under this data-scarce setting: expert elicitation, LLM generation, a data-driven method, and a hybrid method that refines expert and LLM-elicited graphs using data. Our analysis reveals areas of agreement between the graphs, but also contradictions in different tendencies impacting the directionality and inclusion of socioeconomic and clinical factors. Additionally, we show that tiny data sets can be used to empirically validate conditional independencies encoded in these candidate causal graphs, concluding that causal modeling for specialized populations requires reconciling expert and LLM-generated causal discovery with tiny datasets.

## Life-Space Assessment and Dementia

Dementia is a progressive decline in cognitive functions that can negatively impact the medical, social, functional, and psychological well-being of a patient, ranging from memory loss to depression to social withdrawal. As the average life expectancy and aging population increase, dementia diagnoses will rise as well.

Persons Living with Dementia (PLWD) can be studied by assessing their life-space mobility, which captures a person's physical and social environment, movement, and daily activities. A decrease in life-space is associated with various measures of declining health in older adults, including cognitive decline.

Life-space mobility is primarily measured through the Life-Space Assessment (LSA), a written survey that quantifies an older adult's geographic area in environmental zones and captures the rate at which they travel throughout the day. However, LSAs have primarily focused on urban populations, limiting their applicability to rural or Indigenous settings where dementia risk is higher.

## The Challenge: Causal Modeling with Tiny Data

- **Causal modeling is necessary for intervention.** While life-space is an effective indicator of quality of life, developing interventions to improve outcomes requires causally modeling its relationship with relevant demographic and environmental variables.
- **Data paucity limits causal discovery.** Data-driven causal discovery methods exploit patterns in large amounts of high-dimensional data, along with assumptions about the underlying causal dynamics, to induce causal graphs. However, the paucity of data about understudied populations makes these methods difficult to apply.
- **Hybrid approaches rely on domain knowledge.** In low-data settings, hybrid approaches use smaller datasets to refine graphs derived from incomplete domain knowledge, obtained either from domain experts or from LLMs. LLMs are useful in this setting because they can capture correlations over causal facts from their vast training corpora.
- **Good initial causal graphs are difficult to obtain.** Each of these approaches depends on good initial causal graphs, which are difficult to construct in understudied domains.

## Dataset

We constructed a dataset from LSAs of 20 patients conducted in rural and Indigenous communities in northern Minnesota, USA, and Ontario, Canada. Nine boolean features were extracted from the LSA, demographic data for patients and caregivers, and daily diaries completed by the caregiver over the course of a month.

<table style="margin-left:auto;margin-right:auto;">
  <thead><tr><th>Variable</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>LS</td><td>Life-space score</td></tr>
    <tr><td>PS</td><td>Sex of the patient</td></tr>
    <tr><td>CS</td><td>Sex of the caregiver</td></tr>
    <tr><td>PE</td><td>Education of the patient</td></tr>
    <tr><td>CE</td><td>Education of the caregiver</td></tr>
    <tr><td>CT</td><td>Community type</td></tr>
    <tr><td>ND</td><td>Number of non-routine days</td></tr>
    <tr><td>CD</td><td>Number of challenging days</td></tr>
    <tr><td>TB</td><td>Total burden on the caregiver</td></tr>
  </tbody>
</table>
<br/>

Continuous variables were binarized using expert-provided or sample mean-based thresholds.

## Methods

We consider four types of causal graph construction methods:

1. **Expert elicitation.** Candidate causal graphs obtained from multiple experts' consensus.
2. **LLM generation.** Graphs generated by three LLMs — Claude (4.5 Sonnet), Gemini (3 Thinking), and ChatGPT (GPT 5.2) — each prompted five times with the variables and their descriptions. Graphs were pooled by adding causal edges in decreasing order of their average weight, excluding edges that introduce a cycle or fall below a weight threshold.
3. **Data-driven discovery.** The Fast Causal Inference (FCI) algorithm applied as a purely data-based baseline.
4. **Hybrid subtractive refinement.** Refines the above graphs by deleting edges to optimize the Minimal Description Length score.

<div align="center">
  <img src="/assets/images/project/Lifespace_fig.png" width="760" /><br/>
  <i>Fig. 1. The causal graphs for the Life-space Domain. (a-c) shows the causal graphs provided by the different LLMs, (d) shows the consensus (common causal relationships) across the different LLMs, (e) shows the expert causal graph, and (f) shows the consensus between the LLMs and the experts.</i>
</div>
<br/>

## Research questions

### Q1: Is there any consensus in causal relations identified by experts and LLMs?

The LLMs agree on six direct causal relationships: Non-routine days (ND), community type (CT), education of caregiver (CE), and life-space score (LS) are direct causes of total burden (TB); challenging days (CD) and community type (CT) are direct causes of life-space score (LS).

While experts agree with the LLMs on five of these six relationships, they invert the final edge, placing the causal direction from TB to LS. This disparity suggests a fundamental difference in modeling perspectives: the experts appear to be more interested in patient outcomes, treating the life-space score as the final sink node, while the LLMs consistently identify the caregiver's total burden as the ultimate sink variable. This disparity might also point to the bidirectional nature of the relationship, requiring a disaggregation across time.

Further, the LLMs exclude socio-economic factors such as sex and education, which the experts identify as significant causal drivers.

### Q2: Are the graphs obtained from experts and LLMs compatible with the statistical patterns in the tiny dataset?

The number of edges deleted during the hybrid refinement process serves as a measure of compatibility between causal models and the dataset. Refinement eliminated nearly all edges, leaving fewer than three in the final graphs. The data-driven baseline did not identify any causal edges, but did identify three undirected associations: caregiver's sex with patient's sex, caregiver's education with community type, and challenging days with total burden. These results indicate high incompatibility between the tiny dataset and the LLMs' and experts' graphs.

We further analyze this incompatibility by empirically evaluating the conditional independence (CI) relations entailed by each graph, treating each network as a model that predicts whether variables X and Y are independent given a variable Z. Predictions are evaluated against data-driven labels using the G-test (α = 0.05, conditioning set of size at most one).

<table style="margin-left:auto;margin-right:auto;">
  <thead><tr><th>Model</th><th>Total CIs</th><th>Precision</th><th>FPR</th></tr></thead>
  <tbody>
    <tr><td>Expert</td><td>113</td><td>0.73</td><td>0.53</td></tr>
    <tr><td>GPT</td><td>45</td><td>0.67</td><td>0.48</td></tr>
    <tr><td>Claude</td><td>45</td><td>0.73</td><td>0.39</td></tr>
    <tr><td>Gemini</td><td>23</td><td>0.70</td><td>0.33</td></tr>
    <tr><td>LLM Consensus</td><td>31</td><td>0.68</td><td>0.48</td></tr>
    <tr><td>Overall Consensus</td><td>39</td><td>0.72</td><td>0.52</td></tr>
  </tbody>
</table>
<br/>

The expert graph entails more CIs than the LLM graphs, resulting in higher or equal precision but a higher false positive rate. The LLM graphs entail fewer independencies overall, but still entail independencies incompatible with the data. Claude's graph has a lower FPR and the same precision as the expert graph, while entailing less than half the number of independencies.

Neither the LLM-generated graphs nor the expert-constructed graphs are compatible with the data; however, they are incompatible in different ways, illustrating the structural differences between expert and LLM-based causal models.

## Conclusion

We considered the problem of causally modeling the life-space mobility of people living with dementia in non-urban environments. The domain's understudied nature and the resulting data paucity make this a challenging problem. We considered two additional sources of causal knowledge: domain experts and LLMs. While data-driven causal discovery and refinement of expert and LLM-elicited causal graphs proved unsuccessful, the tiny dataset allowed us to compare the two types of graphs.

The graph structures reveal distinct underlying assumptions. Experts prioritized patient-centric outcomes and integrated socio-economic factors like sex and education into the causal structure. In contrast, the LLMs focused on the total burden and ignored socio-economic factors. Our analysis of the differences among sources of causal knowledge — domain experts, LLMs, and tiny datasets — provides a foundation for hybrid causal models. Understanding the interplay between expert-led and LLM-driven discovery remains essential for developing robust clinical decision-support systems.

## Citation

If you build on or use portions of this work, please cite:

```bibtex
@inproceedings{singh2026lifespace,
  title     = {Causal Models with Tiny Data: The Case of Rural People Living with Dementia},
  author    = {Singh, Ranveer and Mathur, Saurabh and Komarasamy, Kavimayil P.
               and Soni, Ameet and Whetung, Cliff and Warry, Wayne
               and Jacklin, Kristen and Blind, Melissa and Natarajan, Sriraam},
  booktitle = {Proceedings of the 24th International Conference on
               Artificial Intelligence in Medicine (AIME)},
  year      = {2026},
  note      = {Supported by NIH awards R01NS133142 and 1R21AG072566}
}
```

## Acknowledgements

We gratefully acknowledge the support of NIH awards R01NS133142 and 1R21AG072566.
