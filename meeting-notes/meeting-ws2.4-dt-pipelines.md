---
tags: meeting
description: WS2.4 - Reproducible pipelines
---

:::info
**Live notes on hackmd**: https://hackmd.io/@turing-es/Hy6kj78Qa

**Contents**
[TOC]
:::

---

```
<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->
# Meeting 2023-10-31
## Attendees
## Apologies
## Notes
<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

```
==Actions are highlighted yellow==

# Meeting 2023-12-04
## Attendees
- Cass Gould van Praag (Turing)
- James Byrne (BAS)
- Colin Sauze (NOC)
- Alejandro Coca-Castro (Turing)
- Bryn Ubald (BAS)
- Sara Bernardini
- Jenifer Durden
- Eric Daub

## Apologies
- Harry Meacher
- Kalle Westerling

## Notes
**Call recording**: Not available as no host permissions :(

### HIAG FRAS MPA
- Interesting marine life which doesn't live anywhere else in the celtic sea
- Video [vimeo.com/272607634](https://vimeo.com/272607634)
- Use case for DT: Conservation monitoring for joint nature ==...==
    - Assess biodiversity changes and design future missions
    - Collating information already available
    - Not just rebranding of another model already existing
### Main data sources
- ![Screenshot 2023-12-04 at 09.10.58](https://hackmd.io/_uploads/SyeAjvzjr6.png)
- ![Screenshot 2023-12-04 at 09.12.10](https://hackmd.io/_uploads/SyBxOMjH6.png)
- ![Screenshot 2023-12-04 at 09.12.55](https://hackmd.io/_uploads/SkMm_fsST.png)
- Tif images broken down into individual tiles, which can be requested by header. Means don't have to retreive all image
- ![Screenshot 2023-12-04 at 09.13.55](https://hackmd.io/_uploads/BkALuMiHT.png)
- Flatgeobuf didn't work as well 
- MBtiles worked quite well 
- ![Screenshot 2023-12-04 at 09.14.56](https://hackmd.io/_uploads/ry3q_MsSa.png)
- Tile server required to sit between the tiles and server rather than querying the object store directly
- ![Screenshot 2023-12-04 at 09.15.44](https://hackmd.io/_uploads/HyCTOfsrT.png)
- Spatio temporal asset catalogue (STAC)
    - Written with .json. 
    - Doesn't require specific API
    - ![Screenshot 2023-12-04 at 09.17.15](https://hackmd.io/_uploads/ryDXKfsHa.png)
    - For each image there is a stac entry. Can retrieve metadata directly from catalogue, and image thumbnail.

### Data analysis in real time
- biodiversity calcualtions on csv data
- Needs to be done with an API rather than on client side (difficult to transfer to client) - stateless and containerised
    - Handles interactions from user interface
    - Could work via a bot, but not specifically designed for this
    - Developed with unpublished data and restricted access (OAuth with ORCiD and Office 365)
        - No fine grain auth control - all or nothing access
        - Would like to include depositor specified individual access - not yet developed
        - ![Screenshot 2023-12-04 at 09.20.52](https://hackmd.io/_uploads/SkkbczorT.png)
- Deployed with GitLab CI
- Experimental deployment onto Oracle cloud when Jasmin went down
    - found some important and Jasmin specific bugs
    - developed Selenium tests - testing website by pushing buttons on website.
- Architecture overview
    - ![Screenshot 2023-12-04 at 09.22.03](https://hackmd.io/_uploads/SJuHqGsB6.png)
    - Some preprocessing on data files to get to required formats (.json, geotiff etc.)
    - Creating cloud optimised files
    - Creating stac catalogue
    - Sorted on jasmine object store
    - Front end java script and react
    - Gitlab code populates containers
- Asset register for DT
    - Data and code => recipe for DT
    - Currently being populated - records written but not public
- Live demo ==ACTION: Colin if her can record and share something?==
    - ![Screenshot 2023-12-04 at 09.27.01](https://hackmd.io/_uploads/rkWuozsrp.png)
    - Add/select layers of interest
    - Run API queries for analysis
    - 3D interface based in ==cesium (?sp and link)== library - not fully developed, just exploring feasability with library

### Questions
- Sara: Is it public to use by anyone?
    - URL is public, but would need to be added to auth and access restricted data sets
- Sara: How do you envisage users to use it?
    - This prototype
    - Select group of people with guidance (==JNCC ??==)
    - Use case = exploring the data people have got, design future surveys
        - Jen:
            - Conservation aims specific to this sight. What information they needed: e.g. diversity of organisms, invasive species monitoring, conservation interest species, "how can we survey more efficiently for the oney we have". 
            - Testing statisitical robustness - chosing parameters - how many pictures do we need to take in order to make an appropriate sampling unit (power calculations?). Based on existing data sets.
            - Specific conservation aimd made generalisable, so could transfer to a new site.
- Sara: DT => updating of the modle. Is there continuous update:
    - Jen: Survey updated every 3 years. Public data are updated more regularly. These are enormous datasets which need to be manually filtered for area and taxonomy - no continuous update of model. Balancing appropriateness of user queries
- James: How are you managing the workflow?
    - Varied by tile type - differnt scripts for differnt file types
    - No explicit worksflow management system for this size of data
    - An army of data manager would have been useful!
- Alejandro: What motivated the STAC catalogue? Vector format issues - considered other options e.g. x-array? Would a single ecosystem be more sustainable? https://xvec.readthedocs.io/en/stable/
    - Concern about the number of libraries we are using and the sustainabilitiy risk for each
    - Some librabries interact with the STAC catalogue. May be used to drive the web interface, but we used 
    - Jen: Variety of inputs and outputs was a challenge
- Sara: DT decision making?
    - Design of surveys and conservation monitoring
    - this would be a single data point in a large ocean DT
    - We don't have a strong mechanistic understanding of how phenomena effect the organisms, so can't model/predict that effectively yet.
    - Managing human impacts comes less from a data directed approach. Looking to develop a standard framework/template which people can build off.
    - Lots of conversations about whether DT is appropriate framework for this
    - An autonamous vehicle doing constant monitoring would be great, but don't have the momney for that! Looking to reduce spending on surveys!
- James: A lot of the conservation applications (e.g. with WWF) are individual end-to-end pipelines for single usecases, and trying to make them generalisable. Colin and James have been discussing shared technical issues. There are limitations in the indivual use cases, but they can be informative to others .Important thing is theta we start to converge on the pipelines and share the technology. 
- Jen: DT using telemetry data on organism trackers, but that's n=1. To make conservation decisions need large n. Does daily updating matter based on the decsision your trying to make? Is it worthwhile updating more frequenctly?
- Colin: The system is scalable for more frequent updating (but might run outof object store!)
- Sara: Could you use this tool to simulate a future unexpected efvent? Although you don't have much understandong of how the speciies may be effected?
    - Jen: IPCC prediciiotns could be used to move towards correlation (but not causation) analysis. We don't have good causative understangin. Ideally federate DT of seabed with EU climate DTs, but leads to huge problems of scale. 

## Next presenter?
- ![Screenshot 2023-12-04 at 09.57.00](https://hackmd.io/_uploads/SJdufQiST.png)
    - ==Who on these projects?==
- Tom anderson talk 
- ==Eric for DT Base?==
- ==Meeting on 18th?== Suggested we don't have this one
- ==Cass action the above with Harry==




<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

# Meeting 2023-11-20
**Call recording**: [link](https://thealanturininstitute.sharepoint.com/:v:/s/ESGrandChallenge245/EVEJnHyAUOFJrRxAOOInCQsBoryOmwJZhdLRDRbnjns6xw?e=nMNXyR)

## Attendees
- Cass Gould van Praag
- Sara Bernardini
- Harry Meacher
- Bryn Noel Ubald
- Colin Sauze
- Kalle Westerling
- Alejandro Coca-Castro
- James Byrne
- Mafalda Cunha
- Daniel Delbarre
- Jennifer Durden
- Veerle Huvenne

## Apologies
- Markus Hauru
- Oliver Strickson 
- Greg Mingas

## Notes

### New intros
- Bryn Ubald, new RSE as BAS (IceNet and others)
- Veerle, NOC
- Alejandro Coca-Castro, Turing Research Fellow (many project connections)
- Kalle Westerling, Turing RAM (TRIC-DT, DeepSensor)
- Jen Ding, Turing RAM (Clim-Recal, DyME)

### IceNet (James Byrne)
[RECORDING OF JAMES'S PRESENTATION](https://thealanturininstitute.sharepoint.com/:v:/s/ESGrandChallenge245/EVEJnHyAUOFJrRxAOOInCQsBoryOmwJZhdLRDRbnjns6xw?e=nMNXyR
)
- ==[Slides - James Byrne presenting...]==
- Sea Ice forcasting system developed at BAS
    - Sea ice conentration prediction system, AND
    - Example of an environmental predicti0on system => generalisable
        - Never build something twice if you can code it!
- IceNet Onion
    - ![image](https://hackmd.io/_uploads/Bkzn9RO4a.png)
        - Model: The producer(s) of research data products.
            - How do we make the product opporationally useful
            - increase utility to researchers
        - Pipelines: The operational layer providing tooling, automation and simplifying model usage.
        - Infrastructure: Enabling access and to products and services providing by pipelines.
        - Digital Ecosystem: Building interaction through standardisation and FAIR access to infrastructure.
- Need to think about the whole ecosystem which this tool exisits in
    - DTs are systems of systems = an ecosystem
- Model
    - Key characteristics:
        - 1) IceNet functionality implemented in an dedicated Python library...
            - PIP installable
        - 2) ..designed for usage of agnostic Al/ML backends, promoting research...
        - 3) ..promotes code decomposition into generalised libraries, decouples researchers from operations and focuses documentation on SIC forecasting.
- ==[Original paper](https://www.nature.com/articles/s41467-021-25257-4)==
- Now a daily forcasting system. Easy to experment with different resolutions
- AI behind IceNet is continutally developing with researchers actively contributing to model development
    - IceNet AI: the future
    - Things to note:
        - Models can change significantly, without changes to the rest of the layers
        - Researchers can focus on key issues with forecast accuracy, resolution and certainty
        - New model methods are easier to generalise to other prediction systems
        - Understanding how to deliver and use forecasts is as important as improving them: both need to happen
- Pipelines
    - Way of using the model library
    - Key characteristics:
        - 1) Pipelines exemplify operational workflow implementations simply, with bash...
            - Users can extract production usage away from the research
            - Transitioning ML into an opporationsal setting (don't nwed to be a ML researcerh to apply)
            - Can think about ensambling and running over multiple clouds/HPC/hosts
                - Currently running on BAS and JASMIN HPCs with GPUs
            - Asset generation, e.g. for reporting: outputs, observations, predictions and comparative analysis - peroduced when the model is trained
        - 2) ...examples applicable to researchers, operational and support staff alike...
        - 3) …provides scaling up and integration through:
            - 1) Multi-environment setups, configuration-driven
            - 2) Workflows, ensembling and interfacing for self-service and systems integration
            - 3) Decoupling of multi-tenant, modelling lifecycles
    - ![image](https://hackmd.io/_uploads/SJui3COET.png)
- Infrastructure
    - Key characterics
        - 1) Cloud based infrastructure that handles assets produced from any pipeline..
        - 2) ...decouples underlying pipeline / model implementations from services / products..
            - Data and assets can be moved out of the host
        - 3) ...acts as the first user-focused layer, where **researchers, administrators and support staff are insulated from complexity**: giving rise to asset adoption and self-service potential.
            - 
    - Old diagram for infrastructure:
        - ![image](https://hackmd.io/_uploads/SJCc6Ru4a.png)
    - This is what it has turned into:
        - ![image](https://hackmd.io/_uploads/SJW6pRuNa.png)
        - Azure-based cloud service
        - Zero-trust ETC processing:
            - ![image](https://hackmd.io/_uploads/HkZx00_ET.png)
- Digital Ecosystem
    - Long term vision for how the infrastrucutre can be aligned to IMFe. Standardising infrastrcuture so it can be interoperable. 
        - Demonstrating and applying this infrastructure to multiple use cases
        - Capturing how that's influencing other projects
    - Key characteristic
        - 1) Long term vision for digital infrastructure drives standardisation, governance and interfacing with environmental prediction systems..
        - 2) we develop consistent interfaces and governance across infrastructures..
        - 3) ...through demonstration, integration and real-world application, we highlight the benefits of considering eventual Digital Twin ecosystems.
    - Long before IMFe, this concept of the infratructure was created:
        - ![image](https://hackmd.io/_uploads/HJ02AAON6.png)
    - Use-cases: AMOP
        - IceNet forms part of the data feed for navigation of Sir David Attenborough route planning
        - ![image](https://hackmd.io/_uploads/B1FGyyFNa.png)
            - Interesting point: source data is same as that used for IceNet for training, prediction, and testing = generalisability of tooling from day 1
    - Heavily influential piece: IMFe for Environmental DTs
        - ![image](https://hackmd.io/_uploads/SyYwJ1KET.png)
        - Asset Register has come out of IMFe -- can be fed into the digital twin, linking all the DT components together for interoperability.
            - Broad awareness of digital ecosystem is valuable 
    - Pipeline layer earlier = all embedded within the overall DT component, together with a bunch of other things (research, EDS Book (publishing), MLOps, etc.)
        - ![image](https://hackmd.io/_uploads/Byk3ykF46.png)
    - takes a lot of code-bases to give rise to IceNet (see orange on top left)
    - ![image](https://hackmd.io/_uploads/SyJJgytNp.png)
    - interoperability:
        - ![image](https://hackmd.io/_uploads/H1GmxyF4a.png)


### Questions
- Colin: What did you use to produce the diagram of the network infrastructure?
    - James: Draw.io
    - Cass: You might like [kumu](https://kumu.io/) for creating system maps
- Jenn Durden: Specialist in real-world application. How much expert knowledge needs to be included? Where do we choose to disconnect intentionally - make sure people are 'playing' in an appropriate/safe way? How do I do the ground truth checking if I don't know what's going on?
    -  James: Communication between technical specialists and users - they drive the requirements. 
        - Don't "build it and they will come" -- build things that matter for end-users/researchers. Have a clear discussion about the requiremenst and how the technical products and services we offer can be best used to meet their needs. 
    - Jenn: We are heavy on the technical in this group - how are we going to engage the end users?
        - Cass: Mapping people and projects in a stakeholder map. That will help us find users and communities. Then we have events and outreach. WS2.4 might want an event as well. We have resources to do so. Effective for community processes and outcomes that you might want to create for this.
        - Jenn: Let's not do it as event, but as part of the process. Risk with separating this out as a separate WS.
        - Cass: Many projects need to understand their own management of their tools and communities. Capacity-building, creating engagement roots. How do we get people to think about users all the way through?
    - James: What are the objectives for WS2.4? 
        - **Guiding principles** around development of tool with end users centred throughout
        - Jenn: Makes sure users time is appropriately compensated and time allocated
            - Harry: Scoping WS up to March 2024 - this learning can be incorporated
    - Kalle: Careful how we may be conflating "users" with "stakeholders". 
        - Jen Ding: stakeholders at what level? Project, GC, other? Is there a priamry user we are centering for 2.4?
            - Sara: We are still trying to define the techicanl work of the WS.
                - Cass: We could define lessons learnt over the course of our projects, for success and how to overcome challenges.

![image](https://hackmd.io/_uploads/ByJX4JKVp.png)
- WS2.4 cuts across the whole E&S Grand Challenge 

- Next steps for IceNet
    - We have a rich landscape of digital assets. See if we can cross-inherit over them.
    - Provide tools to shortcut their infrastructure navigation - surrounding layers of onions - making them more capable. 
    - We shouldn't try to interfere with the ongoing research, just the assets which are more adaptable.

- Sara: What are the specific challenges we're trying to face as a group. Identify commong challenges. Perhaps bring more scientists into this team (we might be quite infrastrucutre/technical heavy)
- Jenn: Data culture and research culture varies accross our landscape.

- Colin presenting next meeting: Monday 4th December 09:00-10:00

<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->

# Meeting 2023-11-06

## Attendees
- Sara Benardini (Chair)
- Harry Meacher
- James Byrne
- Markus Hauru
- Colin Sauze
- Eric Daub
- Mafalda Cunha
- Oliver Strickson
- Daniel Delbarre
- Jen Durden

### Apologies
- Alejandro
- Rebecca Ward (this time doens't work for her)
- Jen Ding (TBC)
- Veerle Huvenne

## Notes
- Purpose of today is mainly introductions and setting plans for next sessions
- Buld on what's been done in the past and build new capabilities
    - Importannt to know what's been done in your instutions so we can build on it!
- GC funding until March 2024, then expect sustained funding going forwards
- Not clear if we will be submitting bids (likely)
- Looking to itsentify short term wins and what we can deliver in the next round
- Please update your bios and add links
- WS1 is stakeholder mapping - this should surface conenctions and make sure we're not working in silos!
### Introductions
- Sara 
    - Leading 2.4, participating in WS2.1
    - Royal Holloway
    - Research in autonomous systems, AI planning
    - Hiring 2 new people for this project ==roles?==
- Colin
    - Research Software Engineer at NOC
    - Building DT of ==..==
        - Data pipelines, formating data for web interfaces
    - AI for robotic systems, autnonmous surface craft, long term autononmy (gradually degrading components)
    - Built image analysis pipelines for imaging plants.
- Jen
    - NOC
    - Deep sea biologist
    - Use AI to examine sea bed photographs for biodiversity monitoring
    - DT using biodiversity image data 
    - principle focus for this project is QC
        - How do we know that we get a biologically useful answer, not just AI metric to evaulate our outputs
- Harry
    - Programme Manager for E&S GC
    - Working closely with Scott Hoskin as interim director
- Cass
    - RCM
    - Background Neurimaging and open science
- Markus
    - Turing REG
    - REG lead on [DTBase](https://github.com/alan-turing-institute/DTBase), a continuation of the [CROP](https://github.com/alan-turing-institute/CROP) project.
- Eric 
    - Principal Research Data scientist, REG, Turing
    - Computational physicist, earthquake science
    - Leading REG engagement with E&S (also DT:TRIC)
    - Interests in this WS: Reproducibility, data access, capturing research outputs as software
- Oliver
    - Turing REG
    - Primarily on the Met Office collaboration
        - Currently in exploration phase
        - Slightly closed, IP to detail out
    - Talking with Tom Andersson about DeepSensor
        - Lots of video resource from Tom's handover (with Kalle Westerling)
    - MOGP emulator (Software package for  using surrogate modelling for uncertainty quantification)
        - Eric and Oliver worked on this as RSEs
        - big emphasis on sensor placement
        - Currently part of a project in DT:TRIC to understand emulator use more widely as part of Digital Twins
        - Used in a number of environmental contexts, including climate projections for IPCC, tsunami inundation models,
    - Co-lead on amber project biodiversity monitoring on moths and insects
        - Traps to be deployed around the world
        - Collaboration with CH
    - Connected to IceNet
- Dan
    - Turing data wrangler
    - Worked on helathcare and recently moved into E&S
    - Data wranglers work on preparing research-ready datasets
        - Incolrporating multiple sources
        - harmonisation, structuring
        - activities taloired to the project
- Mafalda
    - Impact at Turing
    - =sorry Mafalda! I missed most of this!!==
- James
    - British Antarctic Survey (BAS)
    - RSE lead - hiring 3 people for this GC work, one on board two to follow in Jan 2024
    - Looking at how RSEs fit into BAS as an organisation, establishing sustainable group operations and pushing environmental DRI agendas
    - Leading on reproducible pipelines 
    - Worked on quite a few projects in and outside of BAS (NERC centres, Turing)
        - ML/EO pipelines (e.g. [IceNet](https://icenet.ai))
        - low power systems for polar deployment (e.g. [Lifetime of Halley](https://www.bas.ac.uk/project/brunt-ice-shelf-movement/))
        - involved with SDA related projects (e.g. [AMOP](https://www.bas.ac.uk/project/autonomous-marine-operations-planning/))
        - Working directly on the pathway to [Antarctic Digital Twins](https://www.bas.ac.uk/project/digital-twins-of-the-polar-regions/#about) with the [AI Lab](https://www.bas.ac.uk/team/science-teams/ai-lab/)
        - I work closely with internal infrastructure (on [DRI](https://www.bas.ac.uk/project/environmental-digital-research-infrastructure/)), [polar data centre](https://www.bas.ac.uk/data/uk-pdc/), [research](https://www.bas.ac.uk/team/science-teams/ai-lab/#about) and engineering teams within BAS and act as a software "bridge" from BAS to wider RSE communities
    - Named on WS 2.4 but awareness over all the WS

### Aim In these meetings
- [Proposal](https://docs.google.com/document/d/1h1jB2evqyjR15oEb6NNHvQyXEwxB8UTSiEhZhnSUGnA/edit?usp=sharing) google doc internal only ==add these attendees to permissions so this link can be put in the notes== (HM requested access from SH 06/11)
- Collect tools already developed
- In each session presentation on the tools and a demo, with part focusing on future work
    - What was done and what wasn't done
    - What will be developed from now on, so we can track baseline
    - ==Propose to meet every two weeks initially== - HM sent doodle
        - Specific technical conversations are required
        - ==Meetings will be recorded and shared==
- Activites in the proposal
    - "Automated predictive services, analytic dashboards, technical guidance" ==add more form doc==
- How can we leverage the tools we have to achieve these goals?
- Presentations in this order (TBC, to be circulated):
- IceNet
    - James
    - Presenting at E&S Knowledge share 29th Nov
    - Can do a dedicated one for this group at the next monthly meeting
- NOC marine protected area (MPA) DT
    - Colin, Jen
- DyME and clim-recal ==(do we need separate talks for these? They are currently part of the same work under Urban Analytics 2.0, but are separate tools)==
    - Jenn Ding and Greg Mingas
    - Either should be able to present these tools
- CROP (DT Base)
    - Markus
- DeepSensor
    - Kalle Westerling
- Harry is setting up a project initialtion document will be set up for each WS. 
    - Who is working on what, how can you connect.

- Presentation logistics
    - Demo style
    - how it could be used by people
    - what would be good to do next
    - ==Cass/Harry: think about how we are going to collect opportunities==
    - 40 min, but interactive throughout
    - Slides to be made available please!
    - Harry will be in touch with a scheduling poll to set the next meeting date

### Events
- Organise a wider event buy the end of March to present some common themes
    - Working up to the next phase
    - Input from others who have done similar!
    - At Turing, invited guests
- This crosses into WS1 :+1: 
- Events and engagement person joining in the next few weeks
- ==Start planning ASAP!==
- Sara is very active in international AI, in lots of conference committees
    - If you are interested in devlivering any activitres in thises spaces, she can introduce
    - Inc AI ==[Bridge programme]()== (not linked to Innovate AI Bridge programme)
    - Would be nice to be seen at the international level

### AOB / Questions / Comments
- Reporting / Governance
    - Eric and Sara co-leading, Presenting at Monthly management meetings
        - 20 min update then disucssing opportunities
    - Would like consistency in reporting across the WSs, including a reporting template (Harry to circulate) ==Note for Cass: check connected with TPS reporting==
        - Actions, blockers, risks.. 
        - Harry will work with Sara and Eric to complete
    - Management meeting minutes will be shared with everyone, and live alongside project initialtion documents
- Project management
    - Each collaborator has a seperate collaboration agreement and deliverables
    - Programme management meeting happening this week 
        - GitHub up for consideration, and MS teams
            - Will make sure any tools used are well integrated


Email update from Alejando: 

For WS2.1 and WS2.4, I've carried out some experimentation of the latest version of DeepSensor for sensor placement of UK soil moisture. The preliminary results replicate the paper I co-authored with Tom Andersoon, 
https://doi.org/10.1017/eds.2023.22, but using ERA5 soil moisture data. My next step is to try the Sim2Real approach which seems to work with real station data, https://arxiv.org/abs/2310.19932

 
    





<!-- %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% -->