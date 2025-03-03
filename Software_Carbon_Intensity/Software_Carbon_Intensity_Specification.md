## Scope

This document, the Software Carbon Intensity technical specification, describes how to calculate the carbon intensity of a software application. It describes the methodology of calculating the total carbon emissions and the selection criteria to turn the total into a rate that can be used to achieve real-wold, physical emissions reductions, also known as abatement.

## References
### Normative References

```
The policy for reference lists is:
1. GSF documents listed should have at least one approved version – draft-only docs should not be referenced.
An exception exists for documents approved with or after the referenced doc is approved (maybe part of the same enabler package). In short – approved docs should not reference unapproved docs.
2. The name + version (no date) for GSF specifications are generally sufficient – dates should be used only if there is a specific reason to limit the usage.
3. References to other affiliate docs should similarly provide sufficient information to uniquely determine the needed document and should provide the appropriate source information.
4. The URL for GSF material (new GSF and affiliate) should always be http://www.greensoftware.foundation
    
Models to use:
	[REFLABEL]	<General Model> "Ref Title", Ref information (source, date, id), URL:http//<ref-source>/ 
	[GSFDOC]	<GSF Model> "GSF Document Title",{ Version x.y,} Green Software Foundation™, GSF <docname>{    <version>}, URL:http//www.openmobilealliance.org/ 

If there are no entries in the table – enter 'none' to be precise.

DELETE THIS COMMENT
```
<table>
  <caption>Normative References </caption>
  <tbody>
    <tr>
      <td><strong>[RFC2119]</strong></td>
      <td>"Key words for use in RFCs to Indicate Requirement Levels", S. Bradner, March 1997, URL:http://www.ietf.org/rfc/rfc2119.txt</td>
    </tr>
    <tr>
      <td><strong>[RFC5234]</strong></td>
      <td>"Augmented BNF for Syntax Specifications: ABNF", D. Crocker, Ed., P. Overell, Janury 2008, URL: https://tools.ietf.org/rfc/rfc5234.txt</td>
    </tr>
  </tbody>
</table>

```
Add/Remove reference rows as needed - DELETE This Row 
```

### Informative References

|||
| ----------- | ----------- |
| **[GSFDICT]** | https://github.com/Green-Software-Foundation/Dictionary |
| **Principles of Green Software Engineering** | https://principles.green |

## Terminology and Conventions
### Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC2119].

All sections and appendixes, except "Scope" and "Introduction", are normative unless they are explicitly indicated to be informative.

```
If needed, describe or declare using appropriate normative references the additional conventions that are used. DELETE THIS COMMENT
```

### Definitions

```
Add definitions in new rows of the following table as needed. The following examples show how dictionary references should be made as well as locally defined terms. This table should be maintained in sorted alphabetic order based on the labels of the terms.

Examples:
	Entity              Use definition #1 from [GSFDICT]
	Interactive Service Use definition from [GSFDICT]
	Local Term          The definition description would be presented directly

DELETE THIS COMMENT
```
<table>
  <caption>Marginal </caption>
  <tbody>
    <tr>
	<td><strong>Marginal Carbon Intensity (I) </strong></td>
	<td>This is the emissions intensity of the marginal power plant which will be turned up if you schedule some compute (e.g. increase electricity demand from the grid) at that moment.</td>
    </tr>
    <tr>
	<td><strong>Carbon Delta (D)</strong></td>
	<td>Carbon difference between an initial and modified carbon intensity. This is an optional parameter used to capture a "what if", by comparing a real number against another situation. This allows quantification of carbon savings by using the SCI to compare two carbon intensities, and faciliates a singular statement of, "Over X predictions made, users on average reduced their carbon footprint by Z %</td>
    </tr>
  </tbody>
</table>

```
Add/Remove definition rows as needed - DELETE This Row

```

Kindly consult [GSFDICT] for more definitions used in this document.

### Abbreviations

```
Add abbreviations as needed. No special notation should be made regarding terms copied from the Dictionary.  
The list should be maintained in alphabetic order. DELETE This Row
```

<table>
<caption>Abbreviations</caption>
<tbody>
  <tr>
    <td>GSF</td>
    <td>Green Software Foundation</td>
  </tr>
</tbody>
</table>

## Introduction

#### Problem Statement

The purpose of this specification will be to enable standardization across industry empowering individuals and organizations to make more informed choices in the software solutions that they pick. This solves the problem of incompatible and opaque metrics that are potentially _gameable_ today making it difficult for the end-consumer to make a choice that is aligned with what they are looking for in terms of meeting their environmental goals when purchasing / using software solutions. It will also help developers and users compare one software solution offering against another on environmental impacts.

#### Applications Of This Specification

The specification can be applied to any software to measure and reduce its carbon emissions by creating a standardized and practical methodology. 

#### Target Audience

The target audience for this are technical stakeholders (e.g. software architects, developers, and maintainers) who ideally can use this as a methodology so that they can understand the characteristics of their software solution and minimize the associated emissions.

## Software Sustainability Actions

All actions that can reduce the carbon emissions of a piece of software fall into one of three categories. The SCI specification intends to encourage more of these actions to be taken in developing software applications.

- **Energy Efficiency**: Actions taken to make software use less electricity to perform the same function.
- **Hardware Efficiency**: Actions taken to make software use less physical resources to perform the same function.
- **Carbon Awareness**: Actions taken to time or region-shift software computation to take advantage of clean, renewable or low carbon sources of electricity.

Carbon aware software will optimize the timing and location of operation to minimize emissions associated with operation. This could consist of moving computation to regions with cleaner grid emissions or delaying jobs to cleaner periods (or a combination of both). Energy efficient software will also run on hardware that requires less energy to operate or the software can be re-architected to require less energy to execute. All combined, these effects are reflected in the total operational emissions. 

## Methodology Summary 

This standard can be used to calculate the real-world emissions associated with software by measuring the total change in global emissions associated with a particular piece of software.

The calculation of software carbon intensity MUST include all supporting infrastructure and systems that significantly contributes to the software operation. Supporting infrastructure and systems MAY include:
- compute resources
- storage
- networking equipment
- memory
- monitoring
- idle machines
- logging
- scanning
- testing
- operations
- backup
The entity calculating software carbon intensity MUST report what is included within this boundary.  

Electricity has a carbon intensity depending on where and when it is consumed. An intensity is a rate. It has a numerator and a denominator. A rate provides you with helpful information when considering the growth of a software product and allows for the computation of a marginal rate.

To calculate the carbon intensity the following information is needed:

`O`= Operational emissions of a given piece of software

`E`= Energy consumed by a given piece of software

`I`= Location-based marginal carbon emissions

`O = E * I ` = Operational emissions based on energy consumption (E) and location-based carbon intensity measurement (I)

`M` = Embodied emissions of a given piece of software
****
**These are used to calculate total carbon emissions (`C`) and carbon intensity (`CI`):**

`C = O + M ` = Total amount of carbon the software is emitting over a time period

`R` = Baseline as a demoninator (e.g. carbon per additional user, api-call, ML job, etc) 

**carbon intensity (`CI`) compares this carbon against a baseline :**

`CI = C / R` = Total carbon intensity rate per baseline

**carbon delta (`D`) is the difference between two carbon intensities :**

`D = CI(initial) - CI(modified)` = Carbon difference between an initial and modified carbon intensity, and is an optional parameter to quantify gains from implementation of Green Software Engineering methods. 



### Operational Emissions  (`O`) 
To calculate the operational emissions associate with software, multiply the electricity consumption of the hardware the software is running on by the regional, granular marginal emissions rate. Because this standard uses a consequential approach, marginal emissions rates should be used for electricity consumption. The marginal emissions rate reflects the change in emissions assoicated with a change in demand. 

#### Energy Measurement (`E`) 
This is a measurement of the energy consumed by a given piece of software for a given task. This must be a measurement of energy consumption in kilowatt hours (kWh) of all supporting infrastructure and systems. This could be applied to several taxonomies:  
- Datacenter
- Indiviudual machine (e.g. VM/Node)
- Indiviudual service (e.g. API call, ML training job)
- Execution of code 

#### Location-Based Marginal Carbon Intensity Measurement (`I`)
The carbon intensity of electricity is a measure of how much carbon (CO2eq) emissions are produced per kilowatt-hour (kWh) of electricity consumed, for a standard unit of gCO2eq/kWh. This requires 'Marginal' carbon (defined above), and This is the emissions intensity of the marginal power plant which will be turned up if you schedule some compute (e.g. increase electricity demand from the grid) at that moment.

Location-based measures the grid carbon intensity (annual average) of a regional balancing authority. From a developer perspective, only the location-based info is important for having an impact on reducing carbon emissions. This excludes market-based measures, and is distinct from 100% renewable energy claims. 

The only figure that matters if you’re trying to optimize the scheduling of your compute in real-time is the marginal emissions intensity. This is the emissions intensity of the marginal power plant which will be turned up if you schedule some compute (e.g. increase electricity demand from the grid) at that moment.

### Embodied Emissions  (`M`) 
[placeholder]

## Core Characteristics

As the SCI specification matures and develops, these core characteristics MUST remain true.

### The SCI is sensitive to carbon awareness, energy efficiency, or hardware efficiency

- The purpose of the SCI is to encourage actions that reduce the carbon emissions of software. Therefore, the SCI MUST be sensitive to those actions described in this document under **Software Sustainability Actions**, precisely carbon awareness, energy efficiency, or hardware efficiency.
- If an application's SCI is X, and then actions are taken to make the application more carbon aware, more energy efficient, or more hardware efficient, the value of X MUST go down.

### The SCI is easy to implement

To achieve impact at scale, the SCI needs to encourage adoption through ease of implementation.

- Anyone without much experience or training MUST be able to follow the SCI specification instructions.
- Calculation of the SCI MUST be possible without incurring any cost, for instance, for data or services or tooling.
- Where possible, teams SHOULD consider investing more time or money in calculating their SCI number to increase its accuracy.

### Reporting the SCI value

You MUST report the `CI` value and you SHOULD report the `C` value but if you are unable to report the `C` value, you MUST provide a reason for why you are unable to do so.

## Exclusions

Because this standard lays out a consequential methodology for calculating the emissions associated with a piece of software, the following must not be included in the calculation: 

### Market-based Measures 
**“Market-based measures"** are achieved through renewables matching (e.g. PPA for solar near a datacenter) that helps lower the grid carbon intensity for everyone in the area. From a carbon accounting perspective PPAs, RECs etc can allow datacenters to get to “100% renewable”, even if the grid is not 100% renewable 24x7 from a grid perspective. Market-based measures includes, but is not limited to the following: 
- Carbon offsets 
- Electricity Attribute Certificates (EACs) 
- Power Purchase Agreements (PPAs)
- Renewable Energy Credits (RECs)

### Infrastructure Meaures 
**“Infrastructure measures”** including any infrastructure that integrate renewables via a "direct wire connection" (e.g. a datacenter with solar panels on the roof and a battery storage located onsite). This is conceptually closer to a Microgrid, where there is a higher % of renewable energy usage than the local grid carbon intensity.




### Version 1.0

```
This section provides a high level, concise and informative description of the main functionality supported in the initial version of the specification. The description should be brief; the target length should be a few paragraphs. 
When the enabler or reference release is finished, this description should be aligned with the final functionality. 

DELETE THIS COMMENT
```

### Version (x.y)

```
This section should be included for each new major or minor version of the specification.

It should provide a high level, concise and informative description of the new or modified functionality introduced in this version of the specification, compared to the previous version. The description should be brief, and the target length should be a few paragraphs. When the enabler or reference release is finished, this description should be 
aligned with the final functionality differences.

DELETE THIS COMMENT
```

#### Version (x.y.z)

```
Service indicator (z) for the document. It is incremented every time a corrective update is made to the approved document version by the WG. This section should describe the main changes made to the specification at a high level compared to the previous version. The description should be brief, and the target length should be one paragraph.

DELETE THIS COMMENT
```

## Sections As Needed

```
Sections for the normative specification text. Fill in as needed. The following validates the styles used for the headers. DELETE THIS COMMENT 
```

### Example Level 2
(Add text here.)

#### Example Level 3
(Add text here.)

##### Example Level 4
(Add text here.)

<figure>
	<img src="images/governance.svg" alt="GSF governance">
	<figcaption>GSF governance</figcaption> 
</figure>	


<table>
  <caption>Example Table</caption>
  <thead>
      <tr>
	  <th>Item</th>
	  <th>Function</th>
	  <th>Reference</th>
      </tr>	      
  </thead>	    
  <tbody>
    <tr>
	<td>Row 1</td>
	<td>Grid 1,1 data</td>
	<td>Grid 1,2 data</td>	    
    </tr>
    <tr>
	<td>Row 2</td>
	<td>Grid 2,1 data</td>
	<td>Grid 2,2 data</td>	    
    </tr>
  </tbody>
</table>

## Appendix Change History (Informative)

### Approved Version x.y History

<table>
    <caption>Approved Version x.y History</caption>
    <thead>
        <tr>
            <th>Reference</th>
            <th>Date</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>    
        <tr>
            <td>n/a</td>
            <td>n/a</td>
            <td>No prior version</td>
        </tr>
    </tbody>
</table>
