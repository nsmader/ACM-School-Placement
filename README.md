# AmeriCorps Member School Placement Algorithm

## Project Description 

Each year City Year places 250 AmeriCorps Members (ACMs) in 26 Chicago Public Schools to serve as near-peer tutors and mentors. We are building a tool that produces diverse teams with conisderation of ACM commute times, preferences, skills, and school needs.

## Tools and Resources
* R and one of these packages (or roll our own)
  * [gmapsdistance](https://cran.r-project.org/web/packages/gmapsdistance/README.html)
  * [GenSA package](https://cran.r-project.org/web/packages/GenSA/GenSA.pdf)
  * [gaoptim](https://cran.r-project.org/web/packages/gaoptim/gaoptim.pdf)
* Visualization
  * Power BI (can compile R script that runs less than 30 mins)
  * Shiny
  * Knitr
* R Optimization and Cleaning Tips
  * [FasteR! HigheR! StrongeR! - A Guide to Speeding Up R Code for Busy People](http://www.noamross.net/blog/2013/4/25/faster-talk.html)
  * [Cleaning Data with R - Nick Mader](http://nsmader.github.io/knitr-sandbox/cleaning-data-with-R.html#intro)

## Similar Problems (Ranked by Relevance)
* [Nurse Scheduling Problem](https://en.wikipedia.org/wiki/Nurse_scheduling_problem)
  * Simulated Annealing
  * Constraint Programming
* [The Traveling Salesman with Simulated Annealing, R, and Shiny](http://toddwschneider.com/posts/traveling-salesman-with-simulated-annealing-r-and-shiny/) - the code from their github formed the backbone of our simulated annealing algorithm
* [Assignment Problem](https://en.wikipedia.org/wiki/Assignment_problem)
* [National Resident Match Algorithm](https://en.wikipedia.org/wiki/National_Resident_Matching_Program#Matching_algorithm)
* [Stable Marriage Problem](https://en.wikipedia.org/wiki/Stable_marriage_problem)

## Final Product
* ACM survey
* Excel Workbook with ACM characteristics produced by survey
  * Column to manually asign an ACM to a school
* Excel Workbook with School characteristics and desired team characteristics
* Google Maps API calls to calculate commutes (DONE!)
* Dashboard for reviewing results
* Built to be as transferable between sites as possible 

## Constraints
* Firm Constraints
  * CMs serving in High Schools must be 21+ or have some college experience
  * Roommates cannot be on the same school team
  * Managers can hand-place individual ACMs into schools, and those placements will be firm constraints
* Soft Constraints
  * Commute times for each ACM are reasonable
  * Consistent gender ratios across all teams
  * Consistent ethnic representations across all teams
  * Consistent tutoring experience across all teams
  * Consistent educational attainment across Elementary Schools (3rd-8th grades) and across High Schools (9th grade)
  * ACM grade level preferences taken into consideration
  * ACM school preferencese taken into consideration

## Inputs - Two Spreadsheets
#### ACM Characteristics Survey (feeds into spreadsheet that includes a column for manual school placement):
Characteristic | Response Options
---------------|------
Did you attend a CPS school? If so, which? | 
Language speaking abilities | 
Age | 
Tutoring experience | 
Tutoring preference | Math, ELA, No Preference
Grade level preference | 
Race/Ethnicity | 
Education level | 
Gender | 
Roommates | 
Home Address | 
Commute Method | Driving, Transit

#### Spreadsheet 2: Characteristics of Schools
Characteristic | Notes
---------------|------
School Type | Elementary or High School
Grade Levels Served | 3, 4, 5, 6, 7, 8, 9
Racial/Ethnic distribution | Necessary? Are we optimizing for demographics that are balanced across the corps or that reflect student demographics?
Linguistic Needs | 
Math Ability Needs | High Schools need stronger math ability
Address (commute times) | 
ACM start and end times (commute times) | 

## Output 1
CM | Placement | Average Commute | Ethnicity | etc.
---|-----------|-----------------|-----------|-----
Name | 1 | 45 | White 

## Unnecessary but Nice Components
* Smart Initial Placements
  * The initial placement method used in the original algorithm simply places any ACM at any school. However if we instead initially place ACMs in a smarter way, we may reduce the number of iterations to reach convergence.  Might look like cycling through each school and adding one ACM at a time.  The ACM might be chosen from a distribution of ACMs meeting certain criteria.
* Smart Swaps
  * As written, the algorithm makes random swaps between all ACMs and makes swaps until it makes positive impact on the residual.  If the algorithm is changed so that it is smarter about which ACMs it is trying to swap, we might be able to reduce the number of iterations
* Deploy 2nd Year ACMs & TLs
  * Currently only placement for first year ACMs is possible with the tool. Placement of TLs and 2nd Year ACMs is based on different criteria and is currently a manual process for site leadership. Qualitative data generally unavailable is also used in placing team leaders (like the relationship with the PM), which makes this challenging.

## Development Workflows 
Workflow  | Tools  | Notes
----------|--------|------
ACM Survey | ?  | Gather all necessary info from incoming ACMs
Placement Algorithm  | R  | Implement algorithm for computing commute times (gmapsdistanceapi) and assigning ACMs to school teams
Results Dashboard  | Power BI  | Visualize the results to help communicate them. Once we get everything together, further exploration will be done to see if we can implement the deployment algorithm in a more interactive way.

## Timeline 
Date | Milestone
-----|----------
April 27 | Make decisions on the approach and final product. Begin development of base functionality. 
May 18 | Network call to check in on progress. 
June 23 | Pull all pieces into final product and start extensive testing. 
July 7 | Product complete with demo ready to present to sites across the national network

## Audience & Usage 
Ideally this will be a tool that City Year sites can use on a natioanl scale.  Usage of the tool would look like this: 
### Set Up 
1. Eval Rep would install R Open and necessary packages (and Power BI)
2. Eval Rep would work with Recruitment & Admissions to distribute survey and pull data into the ACM workbook
3. Eval Rep would partner with their site leadership to configure parameters and set weights
### Use 
1. Once the Excel workbook is configured, Eval Rep would just need to open .pbix file in Power BI
1. Ensure that connection is made with the Excel Workbook
1. Refresh the data (thus executing the placement algorithm)
1. Interpret the results, make necessary adjustments, and re-run as necessary
