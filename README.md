# Tealium Presentation
Tag Management System

Special Cases:
Specific classes for no-click elements (every element which is not an anchor <a>)


A TMS is designed to help manage the lifecycle of multiple analytics products through a centralized dashboard. As illustrated in the picture below, Tealium acts as the middle man between a web page and the various analytics services that we send data to. 

Tealium Workflow for Landing Pages
Below are the high-level touchpoints for a typical Tealium implementation. 
ACRONYMS
GC: Group Connect
DCOM: Data Collection and Operations Management (aka the bank)
DNA: GC Data & Analysis (formally S&A)
PM: GC Project Management
TECH: GC Technology
QA: GC QA
WB: the tagging workbook
WORKFLOW
PM reviews experience (preliminary visuals) and accompanying tagging requirements with internal team
PM presents experience and tagging requirements to DCOM. 
DCOM provides feedback on the tagging strategy and provides feedback.
After all parties have aligned on the workbook, TECH makes code updates per WB
DCOM imports WB into Tealium.
QA validates tag firing on QA server, raises defects.
PM coordinates defect triage and assignment
Repeat steps 4-6 until all defects are resolved.
LAUNCH
DCOM validates tag firing in prod
Resources
1. Implementation Documentation
Enterprise Tag Management Tealium Implementation Vendor Guide
Adobe Audience Manager Implementation Guide

2. Slack
Get help. Help others.  
Join the #tealium channel on the digitaslbi-flag team. 

3. Omnibug Chrome Extension

This extension is handy for seeing the Core Metrics, DART and Google Analytics event firing
https://chrome.google.com/webstore/detail/omnibug/bknpehncffejahipecakbfkomebjmokl
Get the Code
The GroupConnect Tech Team maintains a simple core-tealium implementation module. The purpose of the core-tealium module is to help ensure that Tealium implementations are consistent across projects.
https://gitlab.digitas.com/flag/core-tealium/wikis/home
Workbook Preparation
A well-prepared workbook is the foundation for a successful Tealium implementation. As a developer, you will play an active roll in helping to get the workbook 'ready for development'. Here are a few things to consider:
Workbook should match the template found here
Is the workbook complete? Is anything missing or wrong?
Are there any tracking requirements that are not supported by Tealium?
IDs are valid format (alphanumeric, hyphen and underscore are permitted, cannot start with a number, no spaces, case sensite)
IDs are unique (one per page)
Is there a need for tealium-specific classes? 
If you need help reviewing a workbook for completeness, ask for assistance on the Slack #tealium channel
Implementation Considerations
Tealium implementations can only happen after feature development is complete. Parallel Tealium development is discouraged by DCOM
Only links and buttons are Tealium-enabled by default. Form elements, divs, or other elements will need to be handled by DCOM on a case-by-case basis.
Avoid using Tealium IDs as hooks for other functionality.
DART tags won't fire until after the workbook has been imported into Tealium by the DCOM team
Familiarize yourself with the approach for specifying device context
Tealium does not currently recognize `0.0.0.0` as a valid server and it has been inconsistent with recognizing `127.0.0.1`. 
If you run into issues, try using `localhost` instead.
For video:
DCOM needs the page ID before you can enable video tracking. Otherwise, the bactm_CaptureVideoEvents method will be undefined
The current core-video Brightcove player automatically works via the Tealium video plugin that is included in the core-tealium repository. 
Sites that use the old Brightcove Video players require manual Tealium integration. Go here to determine which version of the player your project has
Development Checklist
A peer implementation review is required for anyone new to Tealium

General Checklist
Add the necessary JS files 
Tealium loads on page (check your network console)
The digitalData object exists and all the values are correct
Page load tags fire a single time
IDs are valid format (alphanumeric, hyphen and underscore are permitted, cannot start with a number, no spaces, case sensite)
IDs are unique (one per page)
Classes are used appropriately, if needed
Conversion Checklist
all coremetrics name attributes have been converted to IDs
--Please remove all name attributes and replace with id attributes.  This prevents errors with the tagging processing.
deprecated script references to eluminate.js and cmdatatagutils.js have been removed
cmCreateManualLinkClickTag method calls are removed from the javascript
Any other CM code is removed from javascript (e.g. cmSetStaging, cX)
all data-dart-cat and data-aam-keyval attributes are removed from the HTML
All dart/doubleclick floodlight tags are removed from Javascript and HTML
dart or dartclick classes are removed from the HTML 
Remove all code we don't need
