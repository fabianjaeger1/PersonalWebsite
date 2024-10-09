---
title: "PyCMAP"
tags: ["web"]
author: "Fabian Jaeger"
math: true
# author: ["Me", "You"] # multiple authors
draft: false
hidemeta: false
comments: true
# description: "Daily game that asks you a Fermi question on a daily basis."
description: "Customizing Python Matplotlib Colormaps"
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
    image: "images/pycmap_0910.png" 
    caption: "Main Screen"
    # size: 40%
showToc: true
TocOpen: true
---

## Overview
[PyCMAP](https://pycmap.com/) is a web application that helps academics and data visualization enthusiasts customize and export colormaps for Python's Matplotlib. The platform simplifies the process of selecting effective color schemes for plots.

## Features

- **Customizable Colormaps**: Adjust parameters like hue and brightness to create unique color schemes.
- **Export Functionality:** Easily export colormaps for use in Matplotlib.
- **Configure plot type:** Allow for the selection of multiple types of plot types.
- **Live Preview:** Visualize changes in real-time before exporting.


## Technical Stack
[PyCMAP](https://pycmap.com/) is built on FastHTML, which leverages HTMX for dynamic content updates. User data is stored on a session basis in an SQLite database hosted on Replit. Since FastHTML is built with Python, both the backend and frontend code utilize Python.

## Future Improvements
I am always looking for ways to enhance PyCMAP. If you have any suggestions, let me know. Here are a few upcoming features:
- **Continuous Colormap Picker:** Implementing the ability to select continous color maps for plot types such as Heatmaps and density plots
- **Color Suggestions:** Introducing features that randomize and suggest colors based on your current selection or offer completely new ideas from scratch.
- **Enhanced Plot Customization:** Expanding customization options for various plot types.
- **Data Upload Functionality:** Allowing users to upload their own datasets.