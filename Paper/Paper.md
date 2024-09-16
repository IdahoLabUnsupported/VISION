---
title: 'VISION: Verifiable Fuel Cycle Simulation, Version 7'
tags:
 - Powersim
 - System Dynamics
 - Nuclear Fuel Cycle Analysis
 - Nuclear Fuel Cycle Transition

authors:
 - name: Ross D. Hays
   orcid: 0000-0001-8458-7539
   equal-contrib: true
   affiliation: 1

affiliations:
 - name: Researcher, Idaho National Laboratory, USA
   index: 1

date: 31 July 2024
bibliography: paper.bib

---
# Summary

The Verifiable Fuel Cycle Simulation (VISION) model has been developed to support researchers who need to examine the complex systematic impacts of transitioning from one nuclear fuel cycle to another.  The VISION model uses the System Dynamics methodology incorporated within the [PowerSim Studio](https://powersim.com/powersim-studio/) simulation software to enable tracking and estimation of generation, transmutation, and disposal of nuclear materials over multi-generational timeframes using a range of user-defined scenario parameters. Wtih the release of version 7, numerous improvements are made available both to the core computational methods and to the user interface which result in a smaller computational footprint and much greater flexibility.  Previously identified errors have been resolved, and known limitations have been more thoroughly documented such that invalid conditions do not produce seemingly valid results.

# Statement of Need
Where the initial verisons (1-3) of VISION developed an overall architecture of the nuclear fuel cycle using three pre-defined reactor types, later versions (4-5) introduced a generalized framework that enabled up to ten user-defined reactor, fuel, and recycling types.  Versions 4-5 also developed a comprehensive fuel recipe taxonomy drawing from the Transmutation Data Library (cite) Project.  

Development continued through versions 6 (unreleased) and 7 to make improvements to usability and computational performance while also expanding the capabilities of certain fuel cycle modules.  

# New Features

1. One input file (vs 4)
Data is provided to the VISION model through a series of Microsoft Excel spreadsheets.  This gives the user a familiar interface with which to work, and empowers them to develop their own pre-processing algorithms using either formulae or Visual Basic scripts.  In versions 4 and 5 of VISION, there were four separate workbooks of input data.  Two contained fundamental input parameters for computing radioactive decay and heat- and toxicity-factors.  One contained scenario parameters, and the final contained nuclear fuel recipes.  Because the fundamental input parameters remain constant, they were directly incorporated into the PowerSim model.  The fuel recipes file contained a wide range of pre-defined recipes organized onto several sheets using the aforementioned Transmutation Data Library numbering scheme.  Through use, it was noted that most users did not leverage these pre-defined recipes, but instead focused primarily on their own custom recipes.  Further, absent rigorous workflows, it is a non-trivial process to verify that no impactful changes have been made between different copies of the recipes file.  For these reasons, the recipe definitions simplified to follow a user-defined numbering scheme and were reorganized into a single, flexible sheet within the main scenario parameter input file.  This aids organization in several ways, including by keeping the fuel recipes paired with their scenarios, by removing all unnecessary data, and by eliminating the often-cryptic organization and numbering scheme.

2. Improved reactor module (fuel transition, track by increment, interpolated discharge recipe on shutdown)

# Acknowledgements
 - Brent Dixon
 - Jake Jacobson
 - Gretchen Matthern
 - Steven Piet