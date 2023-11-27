---
tags: meeting

description: WS2.2 Digital Twins of Envrionment Agriculture
---

:::info
**Live notes on hackmd**: https://hackmd.io/@turing-es/S1UoNaPX6/edit

**Contents**
[TOC]
:::

---

```
# Meeting 2023-10-31
## Attendees
## Apologies
## Notes
```
==Actions are highlighted yellow==

<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->
# Meeting 2023-11-21
## Attendees
- Paul Harris (PH)
- Mariya Iqbal
- Harry Meacher
- Dan Delbarre
- Rebecca Ward
- Chris Baker

## Apologies
- Markus Hauru 
- William Brown
- Cassandra G. Van Praag
- Sophie Arana

## Notes
### Data Wrangling - REG Team meeting (DD)
- DTBase data used - relationship with other data sources. 
- Focus was on databases
- Lessons learned from CROP to DTBase; goal - generic structure. 
- ==ACTION - to meet to dicuss modelling==
- RC - started to put together description of data structures needed e,g timeseries (e.g weather), image, automation and control operation section, etc. Mapping data (with feedback from Rothamsted - such as GIS data). They are on the [DTBase GitHub notes](https://github.com/alan-turing-institute/DTBase) 
- CB - Slides PH shared cover the data Rothamsted using/have available. 
- PH - we are currently avoiding our spatial (within-field) datasets (as can be challenging), our focus is on the farm field level time series data only (20 NWFP fields). 
- ==DD - data dictoary could be useful for both areas, use this to build specification.== 

### Blocker
- Collaboration agreement - Need data transfer from Harvest london/Uni of Surrey

### Impacts
- RW: Optimise willow growth vs energy input - costs to a min. CROP (underground) was opposite in some respects. 
- Benefit of DT to them is not clear at this stage. 

### Rothamsted Update
- Set up meetings with REG & DW team
    - PH- To start with looking at NWFP's 15-minute soil moisture, soil temperature and rainfall data in 15 NWFP catchments for use in DT-Base. Will look at 15-minute water run-off data next but water data is more challenging.
    - PH - PDRAs x3 and DS x1 expected to start in Jan24
    - PH - the Digital Twin feedback loop can be used to influence/direct sample design (i.e., answer the what, where and when)

Q - DT vision: RC- To optimise for net zero and increase in yields- coupled with enabling more precise nutritional recipes that can be automated
==ACTION - AIUK fringe event in March 2024; scope this out.== - Event lead and Senior Community Manager to support

Workshop - deepdive on DT for Agriculture. 

DT Network Plus looking to explore this as part of their outreach activities - engage with David Wagg and Janine Coomber

==DD useful output could be an ontology? 
CB - Leverage and find utility of this first. To discuss in more detail

-PH - Visualisation of uncertaintly could be a worthy cross-over piece of work (for CROP and NWFP).

Last meetings actions: Ruchi to respond to Sophie with regards to the project website; creating PID- consistent format for E&S GC; Data wrangling met with REG


# Meeting 2023-10-31

### Attendees
- Chris,
- Ruchi,
- Edwin,
- Sophie,
- Markus,
- Giogio,
- Dan,
- Harry


### Apologies
- Paul, 
- Mariya

## Notes



### Scoping
Last meeting - Paul & Chris discussed products which could be developed.
Postdocs not in place until January, use the time to flesh out RSE components, ways in which we can adapt DT to host data and models.
Start developing our group website - might help scope
Website -
==ACTION== : Webpage presence for the workstream.

2.3 Scivision (aphids and moths)
Wheat data - lots of data available at Rothamsted.

DT based deplyment for Rothamsted, Data Infrastcurue at Rothamsted. Another meeting on Friday 27/10 with some of the softwre engineers and APIs. Clear next steps for Edwin, Markus and Giogio. Getting 1 data dump from Rothamsted website, plug that into DT infrastructre works. Once it has Rothamsted data then can talk about Rothamsted models that can be leveraged and intergrated.
*NOTE (for HM): Ensure REG plan is included in sprint reporting and PID*

RC: CROP built for underground farm, can it be repurposed? MH: Have copied a lot from CROP but some modernization; some frontend aspects copied over, other aspects require more work e.g. on the database side; underground farm had particular bits whereas making generic data now.
Pat is working with the image data, structure will work across Rothamsted, Pats greenhouse, Rebecca Surrey farms, so data dumps from 3 areas good opp to show data infra works across all areas.
Harvest London (Pat leading)
Willow Farms (Rebecca leading);
CB - Rothamsted have Willow Farm & expertise in this area, important to collaborate. *NOTE (HM): WS1 mapping exercise to flag this*

### By 31st March what can be achieved?
All to update / correct please
-Illustrate run the crop yield models
-Opp to go thorugh ways to improve accuracy of yields prediction models by adding more data
-VizAg: Decision Support Tool based on SPACSYS process-based model (PBM)
-Tools for facilitation advanced / rich query expressions
-Simplace open sources framework - Uni of Bonn

RC: Data Infra between the two and do a data curation, would be a realistic goal
CB: Impact has to be of farm scale, showcase the platform and what it provides, can’t just be infra as otherwise could be any grand challenge.
RC: Benchmarking and collaboration could be post march.

LIVESTREAM DATA, couple of deployments,
What are the resources available to get the work done.
Rothamsted - hiring 4 roles, end of Nov interviewing candidates, RRes RSE will work in Jan and hiring
Data Scientist / Sensor technician (x1), and PDRAs (x3) with some combination of coding, ML, Stats, PBMs, in-situ and remote sensing and visualisation skills
Ruchi - Pat (PhD student - leading on modelling), Rebecca - Surrey collaboration (Note She is retiring in March).
==Action:== Share Rothamsted Job Adverts with networks

==Action:== Create a PID, resource mapping
Dan - can help with data
==Action:== Markus and Dan to touch base re databases (TRIC-DT PDRA overlap), Chris B to join too.

<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->