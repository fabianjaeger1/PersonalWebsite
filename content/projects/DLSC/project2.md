---
title: "Finite Basis Physics Informed Neural Networks"
tags: ["first"]
author: "Fabian Jaeger"
math: true
TocOpen: false
draft: true
hidemeta: false
comments: true
# description: "Finite Basis Physics Informed Neural Networks"
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
    image: "fermle.png" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---


 
<!-- [Regression](https://en.wikipedia.org/wiki/Regression_analysis): -->

Although PINNs are a powerful framework to solve many simpler differential equations, they lack the ability to capture the complexity of high-frequency and multi-scale problems, which is sometimes referred to as the spectral bias of Neural Networks. This in turn implies that for increasingly complex problems, the PINNs network size grows rapidly in addition to having a more complex optimisation problem to solve.

To try and mitigate this problem, FBPINNs can be employed. Through a decomposition of the domain into smaller, partially overlapping subdomains, FBPINNs aim to turn the complex global problem into a easier to solve and smaller local optimisation problem. 

<!-- ![homeinfo](images/homeinfo.jpg) -->

The goal of this report is to contrast the two frameworks and reproduce certain aspects of the paper "Finite Basis Physics-Informed Neural Networks (FBPINNs): a scalable domain decomposition approach for solving differential equations". 
