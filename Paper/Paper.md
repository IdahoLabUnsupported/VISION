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
 - name: Idaho National Laboratory, USA
   index: 1
   ror: 00ty2a548

date: 30 June 2025
bibliography: paper.bib

---
# Summary
The nuclear fuel cycle is comprised of all the steps required to produce, utilize, and dispose of nuclear and associated materials to produce power for productive use.  This typically begins with the mining of uranium or thorium ore, its processing, and its subsequent irradiation in a reactor and ends with emplacement of long-lived wastes in a geologic repository.  In between, a wide array of utilization and recycling processes may be applied, which greatly impact the economics, material efficiency, and other stakeholder metrics of interest.  The Verifiable Fuel Cycle Simulation (VISION) model has been developed to support researchers examining the complex systematic impacts of transitioning from one nuclear fuel cycle configuration to another.  This model uses the system dynamics methodology incorporated within the [@PowersimSoftware_2024] simulation software to enable tracking and estimating generation, transmutation, and disposal of nuclear materials over multigenerational timeframes using a range of user-defined scenario parameters. With the release of version 7, numerous improvements are made available both to the core computational methods and the user interface, which result in a smaller computational footprint and much greater flexibility.  Previously identified errors have been resolved, and known limitations have been more thoroughly documented such that invalid conditions do not produce seemingly valid results.

# Statement of Need
The initial release of VISION (version 3)[@RN104] developed an overall architecture of the nuclear fuel cycle using three predefined reactor, fuel, and recycling types. Later versions (versions 4–5) introduced a generalized framework that enabled up to 10 user-defined types.  Versions 4–5 also developed a comprehensive fuel recipe taxonomy drawing from the Transmutation Data Library Project [@piet2010description] that allowed for standardized access to commonly used parameter sets.
Subsequent user testing revealed that, in practice, users did not leverage the bulk of the provided library of fuel recipes.  Instead, they primarily used the five open spots provided for users to define their own data.  Eliminating the hard-coded fuel taxonomy provided an opportunity to both streamline and simplify the model as well as to improve the user experience.  
Further development continued through versions 6 (unreleased) and 7 to improve usability and computational performance while also expanding the simulation capabilities to include the abilities to perform online fuel changes to reactors and to track fuel in a batchwise manner, thereby eliminating underflow errors commonly associated with using floating-point arithmetic for minor fuel constituents.

# New Features

1. One input file (vs four).
Data are provided to the VISION model through a series of Microsoft Excel spreadsheets.  This gives the user a familiar interface to work with and empowers them to develop their own preprocessing algorithms using either formulae or Visual Basic scripts.  In versions 4 and 5 of VISION, there were four separate workbooks of input data.  Two contained fundamental input parameters for computing radioactive decay and heat and toxicity factors.  One contained scenario parameters, and the final workbook contained nuclear fuel recipes.  Because the fundamental input parameters remain constant, they were directly incorporated into the Powersim model.  The fuel recipes file contained a wide range of predefined recipes organized into several sheets using the aforementioned Transmutation Data Library numbering scheme.  However, most users did not leverage these predefined recipes but instead focused primarily on their own custom recipes.  Further, absent rigorous workflows, it is a nontrivial process to verify that no impactful changes have been made between different copies of the recipes file.  For these reasons, the recipe definitions were simplified to follow a user-defined numbering scheme and reorganized into a single, flexible sheet within the main scenario parameter input file.  This aids organization in several ways, by keeping the fuel recipes paired with their scenarios, removing all unnecessary data, and eliminating the often-cryptic organization and numbering scheme.

2. Improved reactor module.
 The reactor module within VISION is responsible for calculating the movements of nuclear fuel through the value-creating phase of the fuel cycle, where the energy is extracted and where the greatest change in isotopic makeup occurs.  This module takes the provided fresh fuel and operational reactor values and computes the amount of energy that can be generated and the subsequent changes to the inventory of the contained nuclear material.  These calculations include the mass of fuel being discharged due to both continued operation of the reactor and by shutdown of aging reactors, as well as hold-up of fuel within reactors that are not operational due to a shortfall in fuel availability.  
Updates to this module in the latest release include a change from a continuous (floating-point) measure of isotopic fuel mass to a discrete (timestep-batch) measure and the introduction of a new dimension to permit transitions from one recipe to another without interrupting operations.  These changes result in faster computation times, elimination of floating-point underflow errors, better isotopic resolution on reactor shutdown, and greater simulation flexibility.
 
3. Improved computational performance.
Previous releases of the VISION model heavily relied on the Powersim VBFunction capability to perform the more intensive calculations within the model by way of an integrated Visual Basic interpreter.  While these functions are exceptionally flexible, they are quite computationally expensive compared to the built-in functionality offered in Powersim.  A comprehensive refactoring was undertaken to eliminate all but a handful of these variables, while the few that remain were either themselves refactored or encapsulated to run only when necessary.  This resulted in a reduction in runtime of over 50% for many scenarios.

These new features were tested in the development of an international transuranic management exercise under the auspices of the Nuclear Energy Agency (NEA) Expert Group on Advanced Fuel Cycle Scenarios [@NEA_EGAFCS_2024].  In this exercise, a 300 year scenario evolves through three phases whereby an incumbent system is initialized, then a transition is made to a flexible transuranic burning scenario that consumes material both from within the modeled country and from a donor country.  Once the material is consumed, a second transition to an equilibrium scenario is made.  This scenario utilizes all of the new features and is shared in the ZZZ branch of the GitHub repository.


# Acknowledgements
Many researchers have been involved in the development of this model from its initial release through to the current version.  In no particular order, this includes 
 - Brent Dixon
 - Jake Jacobson
 - Gretchen Matthern
 - Steven Piet
 - Benjamin Baker
 - Joseph Grimm
 - Christopher Laws
 - Robert Jeffers
 - David Shropshire

 This work was supported by the U.S. Department of Energy (DOE), Office of Nuclear Energy’s Systems Analysis and Integration Campaign and performed by Battelle Energy Alliance, LLC under Contract No. DE-AC07-05ID1451 with the U.S. Department of Energy.

 # References
