# AmeriCorps Member School Placement Algorithm

## Project Description 

Each year City Year places AmeriCorps Members (ACMs) in one of 26 Chicago Public Schools to serve as near-peer tutors and mentors. We are building a tool that will suggest school placements based on various demographic features and school needs. Our current iteration is an Excel Workbook which makes extensive use of VBA, but suffers from poor performance and a clunky user interface.  The goal of this project is to correct these problems using R and Power BI, where the data can be processed in a parallelized way and visualized with greater transparency.

## Final Product 
* Excel Workbook with ACM characteristics, option for setting parameters (and setting different weights), and school characteristics
* .pbix file containing R script which compiles in under 30 minutes (Microsoft's limit for R in Power BI) 
* Google Maps API calls made through Power BI Query Editor 
* Dashboard for reviewing results
* If it were fast, we might be able to get it to interact with slicers in Power BI 
* User will need to install R, but we can build in code for installing all the correct packages 

## Audience & Usage 
Ideally this will be a tool that each City Year site can use.  Usage of the tool would look like this: 
### Set Up 
1. Eval Rep would need to ensure that they have Power BI Desktop & R (MRAN distribution) installed
2. Eval Rep would partner with their site leadership to configure the parameter sheet and set weights
3. Eval Rep would work with Recruitment & Admissions to get ACM data and pull it into the ACM sheet
### Use 
1. Once the Excel workbook is configured, Eval Rep would just need to open .pbix file in Power BI
1. Ensure that connection is made with the Excel Workbook
1. Refresh the data (thus executing the deployment algorithm)
1. Interpret the results

## Development Workflows 
Workflow  | Tools  | Notes
----------|--------|------
Sorting Algorithm  | R  | Will develop and implement algorithm for deploying ACM
Commute information  | Power Query, Google Maps API   | Given School Locations and ACM Zip Codes, will develop a tool for estimating commute time
Results Dashboard  | Power BI  | Visualize the results to help communicate the results. Once we get everything together, further exploration will be done to see if we can implement the deployment algorithm in a more interactive way.

## Timeline 
Date | Milestone
-----|----------
April 27 | Make decisions on the approach and final product. Ideally figure out pieces that can be assigned to individual point people and begin development of base functionality. 
May 18 | Call to check in on progress. 
June 23 | Pull all pieces into final product and start extensive testing. 
July 7 | Product complete with Demo ready to present to sites across the national network

## Inputs - Two Spreadsheets
#### Spreadsheet 1: Characteristics of Corps Members
Characteristic | Notes
---------------|------
Language speaking abilities  | 
Age (continuous) | 
Tutoring experience in Math | 
Tutoring experience in ELA | 
Tutoring preference (Math or ELA) | 
Race/Ethnicity | Distributed to match demographics of each school
Education level | ACMs who have recently graduated from high school cannot serve in high schools
Gender/Sex | Consistent ratio across schools
Roommates | Roommates cannot be on the same school team
Address | To calculate commute time
Commute method (car or public transit) | 
Manual school placement | Managers can hand-place certain corps members

#### Spreadsheet 1: Characteristics of Schools
Characteristic | Notes
---------------|------
Ranked valuations of all CM considerations | Should this be decided as a site or on school levels?
Grade levels served (elementary or HS) | 
Racial/Ethnic distribution | 
Linguistic needs | 
Address | To calculate commute times
School start time | To calculate commute times

Parent | Title  | Description  | Necessary?  
-------|--------|--------------|---------------------
 Configuration Workbook  | Updateable Parameters Table  | Excel-based Parameter Table allows stakeholders to set "ideal" distribution of ACMs by school for each of the input features.  | Yes
Configuration Workbook  | ACM Input Table  | An Excel Sheet for collecting all relevant data on ACMs  | Yes
Power BI  | Estimate Commute  | Use the Google Maps API to estimate ACM commute so that it can be added as a feature  | No
Deployment Algorithm  | Deploys ACMs  | Uses algorithm to deploy ACMs to schools while maintaining several criteria.   | Yes
Power BI  | Visualize the Results  | Power BI Dashboard which translates what has been done into a digestible dashboard.  | Yes
Configuration  Workbook  | Allow for manual specification of zone or school  | A feature of the ACM Input Table.  Would need to be able to assign ACMs schools or zones which the algorithm respects.    | Yes
Deployment Algorithm/ Configuration Workbook  | Return final deployment  | Power BI should return the deployed ACMs to the Excel workbook in a third sheet  | Yes
Deployment Algorithm  | Smart Swaps  | As written, the algorithm makes random swaps between all ACMs and makes swaps until it makes positive impact on the residual.  If the algorithm is changed so that it is smarter about which ACMs it is trying to swap, we might be able to reduce the number of iterations  | No
| Deployment Algorithm  | Smart Initial Placement  | The initial placement method used in the original algorithm simply places any ACM at any school. However if we instead initially place ACMs in a smarter way, we may reduce the number of iterations to reach convergence.  Might look like cycling through each school and adding one ACM at a time.  The ACM might be chosen from a distribution of ACMs meeting certain criteria.  | No
| Deployment Algorithm | Deploy 2nd Year ACMs & TLs | Currently only placement for first year ACMs is possible with the tool.  TLs and 2nd Year ACMs are placed based on different criteria and is currently a very manual process for site leadership. Qualitative data generally unavailable is also used in placing team leaders (like the relationship with the PM) which might make this challenging. | No