---
layout: post
title: 'Metro Building Footprints'
embed_url: 'https://storymaps.arcgis.com/stories/f625c8e59b154b8eb95c7b0fd17c4ac0'
---
*2025 · ArcGIS Pro • Python • Data Wrangling • Automation • Databases*

*A project with Brian Smith, supported by Metro.*

**The problem.** Metro is the regional government for the Portland area, serving over 1.7 million people across Clackamas, Multnomah, and Washington counties. Its Regional Land Information System (RLIS) includes a Building Footprint Database of roughly 750,000 records. Building use is an important attribute for urban planning, but 58.6% of the building use values in RLIS are blank or unknown.

**Research question.** Can we fill out building use in the RLIS dataset using other data sources?

**Data.** The RLIS Building Footprint dataset (building use and building type), the FEMA USA Structures dataset (occupancy classification and primary occupancy), and the boundaries of the three Metro counties.

**What we did.** We built an automated workflow in Python with ArcPy: clip the RLIS and FEMA datasets to a study area, spatially join them, and run a building use algorithm that reads the attributes from both sources and writes a new feature class classifying each building as residential, non-residential, or unknown. Changing the clip boundary let us explore different areas and keep refining the script.

Checking the output showed the algorithm was not always right. On SE Hawthorne, for example, RLIS had a Fred Meyer recorded as Single Family Residential while FEMA correctly had it as Commercial. That led to a second question: how often do RLIS and FEMA disagree about whether a building is residential? We wrote a second script that labels each building as residential according to both datasets, RLIS only, FEMA only, or neither, and reports the amount of conflict for each county.

**What we found.** The two datasets disagree often, and the amount of conflict varies widely by county: lowest in Multnomah County at 33.8% and highest in Washington County at 77.7%. We were not able to fill out the building use attribute, but we produced a much clearer picture of where the data is inconsistent. Next steps would be adding more data sources to the script, finding ground truth data to validate against, and adding commercial categories so the output goes beyond residential and non-residential.

The full story map, with maps, code, and charts:
