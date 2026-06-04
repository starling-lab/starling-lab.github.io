---
layout: splash
classes:
  - narrow
permalink: /papers/RuralDementiaLifespace/
title: "Causal Models with Tiny Data: The Case of Rural People Living with Dementia"
category: precision-health
description: 'by Ranveer Singh, Saurabh Mathur, Kavimayil P. Komarasamy, Ameet Soni, Cliff Whetung, Wayne Warry, Kristen Jacklin, Melissa Blind, Sriraam Natarajan, In AIME 2026'
author: ['Ranveer Singh']
excerpt: '<i>Ranveer Singh, Saurabh Mathur, Kavimayil P. Komarasamy, Ameet Soni, Cliff Whetung, Wayne Warry, Kristen Jacklin, Melissa Blind, Sriraam Natarajan</i><br/>UT Dallas &nbsp;&middot;&nbsp; TU Darmstadt &nbsp;&middot;&nbsp; Swarthmore &nbsp;&middot;&nbsp; University of Minnesota Medical School<br/><br/>{::nomarkdown}<a href="https://starling-lab.github.io/assets/pdfs/AIME2026_Lifespace.pdf" class="btn btn--light-outline btn--large"><i class="fas fa-file-pdf"></i> Paper</a>{:/nomarkdown}'
toc: true
header:
  overlay_color: SteelBlue
redirect_from:
  - /papers/ruraldementialifespace/
  - /projects/ruraldementialifespace/
  - /projects/RuralDementiaLifespace/
---

> We asked domain experts and three LLMs to construct causal graphs for life-space mobility in rural dementia patients. They agreed on most edges, but disagreed on one that reveals a fundamentally different view of what matters most in dementia care. When tested against real data, none fit well — but they failed in different ways.

## Problem: reasoning about interventions without enough data

Developing interventions to improve outcomes requires causally modeling the relationship between life-space mobility and relevant demographic and environmental variables. For rural and Indigenous populations living with dementia, this is a particularly hard problem — the data needed for standard causal discovery simply does not exist.

Life-space mobility captures a person's physical and social environment, movement, and daily activities. A decrease in life-space is associated with various measures of declining health in older adults, including cognitive decline. Yet Life-Space Assessments (LSAs) have primarily focused on urban populations, limiting their applicability to rural or Indigenous settings where dementia risk is higher.

## Approach: four methods for causal graph construction

We study several approaches for building causal graphs (shown in [Figure 1](#fig-1)) under this data-scarce setting, then compare them structurally and evaluate their empirical validity.

<div id="fig-1" align="center">
  <img src="lifespace_graph_construction_method.png" width="760" /><br/>
  <i>Fig. 1.  Causal graph construction methods, including expert elicitation (1), LLM consensus (Claude, Gemini, GPT) (2), hybrid subtractive refinement (3), and a data-driven FCI baseline (4). </i>
</div>
<br/>

### Variables (9 boolean features, n=20)

Continuous variables were binarized using expert-provided or sample mean-based thresholds.

<table style="margin-left:auto;margin-right:auto;">
  <thead><tr><th>Code</th><th>Variable</th><th>Source</th><th>Prevalence</th></tr></thead>
  <tbody>
    <tr><td>LS</td><td>Life-space score (high)</td><td>Life-Space Assessment</td><td>45%</td></tr>
    <tr><td>TB</td><td>Total burden on caregiver (high)</td><td>Caregiver diary</td><td>40%</td></tr>
    <tr><td>ND</td><td>Non-routine days (above median)</td><td>Caregiver diary</td><td>60%</td></tr>
    <tr><td>CD</td><td>Challenging days (above median)</td><td>Caregiver diary</td><td>45%</td></tr>
    <tr><td>CT</td><td>Community type (rural)</td><td>Demographic</td><td>55%</td></tr>
    <tr><td>PS</td><td>Patient sex (female)</td><td>Demographic</td><td>35%</td></tr>
    <tr><td>CS</td><td>Caregiver sex (female)</td><td>Demographic</td><td>65%</td></tr>
    <tr><td>PE</td><td>Patient education (above threshold)</td><td>Demographic</td><td>35%</td></tr>
    <tr><td>CE</td><td>Caregiver education (above threshold)</td><td>Demographic</td><td>50%</td></tr>
  </tbody>
</table>
<br/>

## Findings: consensus, contradictions, and incompatibility with data

The LLMs agree on six direct causal relationships. Experts agree with five — but invert the sixth in a way that reveals a fundamental difference in modeling perspectives.

<div id="fig-2" align="center">
  <img src="LifeSpaceCausalGraph.png" width="760" /><br/>
  <i>Fig. 2. Expert-constructed (left) vs. LLM consensus (right) causal graphs. Gray arrows = shared edges; blue dashed arrows = expert-only socioeconomic pathways; red arrow = LLM-only inverted key edge; greyed nodes = variables excluded by LLMs. The key structural disagreement: experts place <b>TB→LS</b>; LLMs place <b>LS→TB</b>.</i>
</div>
<br/>

> Experts Say
> **Life-space score (LS)** is the final sink.  
> Experts treat LS as the patient outcome to improve — and include sex and education as causal drivers.

> LLMs Say
> **Caregiver burden (TB)** is the final sink.  
> LLMs consistently make TB the ultimate outcome, and exclude socioeconomic variables entirely.

This disparity suggests a fundamental difference in modeling perspectives. It may also point to the bidirectional nature of the TB–LS relationship, requiring disaggregation across time. LLMs exclude socioeconomic factors such as patient sex, caregiver sex, patient education, and caregiver education, which the experts identify as significant causal drivers.

### Empirical validation

We treat each graph as a model predicting conditional independencies (CIs) and test them against the data using the G-test. Since incorrectly assuming independence is more detrimental than missing a true independence, we focus on Precision and False Positive Rate (FPR).

<table style="margin-left:auto;margin-right:auto;">
  <thead><tr><th>Model</th><th>Total CIs</th><th>Precision</th><th>FPR</th></tr></thead>
  <tbody>
    <tr><td>Expert</td><td>113</td><td><b>0.73</b></td><td>0.53</td></tr>
    <tr><td>GPT</td><td>45</td><td>0.67</td><td>0.48</td></tr>
    <tr><td>Claude</td><td>45</td><td><b>0.73</b></td><td><b>0.39</b></td></tr>
    <tr><td>Gemini</td><td>23</td><td>0.70</td><td><b>0.33</b></td></tr>
    <tr><td>LLM Consensus</td><td>31</td><td>0.68</td><td>0.48</td></tr>
    <tr><td>Overall Consensus</td><td>39</td><td>0.72</td><td>0.52</td></tr>
  </tbody>
</table>
<br/>

Refinement eliminated nearly all edges, leaving fewer than three in the final graphs. The data-driven FCI baseline identified no causal edges — only three undirected associations. Neither LLM-generated nor expert-constructed graphs are compatible with the data, but **they are incompatible in different ways**, illustrating the structural differences between expert and LLM-based causal models.

## Open questions

- **Is the TB–LS edge bidirectional?** The disagreement may reflect a genuine feedback loop requiring temporal disaggregation rather than a single directed edge.
- **Can high-disagreement regions guide targeted elicitation?** The structural differences identified here could be used to solicit more focused expert feedback and build better causal priors.
- **How do causal models for rural and Indigenous populations differ from urban ones?** Understanding these differences has direct implications for intervention design in underserved communities.

## Conclusion

Our analysis of the differences among sources of causal knowledge — domain experts, LLMs, and tiny datasets — provides a foundation for hybrid causal models. The TB–LS edge dispute illustrates that LLMs and experts encode meaningfully different assumptions about what the primary patient outcome is and which variables drive it. Understanding this interplay is essential for developing robust clinical decision-support systems in data-scarce, underserved populations.

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
