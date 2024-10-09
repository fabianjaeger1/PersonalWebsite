---
title: "EcoSIXTem"
tags: ["web"]
author: "Fabian Jaeger"
math: true
# author: ["Me", "You"] # multiple authors
draft: false
hidemeta: false
comments: true
# description: "Daily game that asks you a Fermi question on a daily basis."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "images/ecosixtem.png"
    caption: "Main Screen"
    relative: true
showToc: true
TocOpen: true
---

EcoSIXTem was the solution to a hackathon challenge proposed by SIX Financial Informations at the [START Hack 2024](https://www.startglobal.org/start-hack/home) in St.Gallen.

## What is ESG?
ESG stands for Environmental, Social, and Governance. It’s a framework used to evaluate how companies impact the world beyond just financial performance. Investors and consumers are increasingly interested in these criteria, which assess a company's sustainability and ethical practices.

**Environmental Criteria**
This aspect looks at how a company affects the planet. Key factors include:

- Carbon Footprint: Emissions and energy use.
- Resource Management: Efficient use of water and materials.
- Waste Management: Recycling and waste disposal practices.

**Social Criteria**
Social criteria focus on how a company treats its people and communities, including:

- Labor Practices: Fair treatment and diversity in the workplace.
- Community Engagement: Contributions to local development.
- Customer Satisfaction: Product safety and quality.


**Governance Criteria**
This aspect examines how a company is run, covering:

- Board Diversity: Representation in leadership roles.
- Transparency: Open communication about practices and risks.
- Ethical Conduct: Adherence to laws and anti-corruption efforts.


## Why ESG Matters
With growing attention on sustainability, ESG factors are becoming essential for investment decisions. Companies that prioritize ESG often perform better financially and attract more responsible investors. Additionally, consumers are increasingly choosing brands that align with their values, making ESG initiatives crucial for business success.

## What is EcoSIXTem

As the wordplay might suggest, it is a gamified pixel-art eco-system visualisation of your ESG score for your portfolio. This allows investors to quickly grasp the system's health through distinctive icons and tilesets that represent the four key areas: Growth, Environmental, Social, and Governance factors of the portfolio. 

At the core, each fund is represented by a tree. The growth of an asset is visualised through arrows pointing up or downwards, for increasing or decreasing values respectively.

For the **environmental factor** we chose a dead tree, polluted clouds and a desert tile on the floormesh to represent a bad environmental score while on the opposite side of the spectrum we have a healthy green tree, normal white clouds and a grassy tile.

For the **social factor** we chose the use of wild, uncultivated or undesired animals or insects such as the bug or wolf to represent a bad score and typical domesticated animals, such as the chicken and sheep, for a good score.

Lastly for **governance** we decided on describing it by the amount and type of debris/ground clutter found, such as random branches, rocks and twigs for a bad score and cultivated and well-treated bushes and plants for good scores. At the same time we have a park ranger that is meant to look after and protect the ecosystem.


![Overview of ecoSIXtem](images/overview_ecosixtem.png)


## Tech Stack

Below is an overview of the used Tech stack. The backend consists of data preprocessing in python of a ESG manufacuters list in a `.csv` provided by the challenge, that lists out the different scores for each of the companies. This preprocessing is combined in a Flask server that also communicates with the SIX API to retrieve relevant information about the asset such as current price and growth numbers.

![Overview of Tech Stack](images/architecture.png)