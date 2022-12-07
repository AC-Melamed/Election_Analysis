Module 3 Deliverable 3
# Election Analysis


## Overview of Project 
The project consists of a program written in Python 3 for the purpose of analyzing a corpus of data documenting the votes tallied for a recent local congressional election.  The data was provided in the form of a .CSV file indexed by "Ballot ID", "County", and "Candidate" with the request that the results of the analysis performed be automatically printed to a .TXT file in a simple readable form by the Python program.  Both the data corpus and the analysis are included in this repository alongside the program script.    

## Resources
- Data Source: election_results.csv
- Software: Python 3.6.1, Visual Studio Code, 1.38.1

### Purpose
The purpose of this project was to perform a simple audit of the election data to confirm various results.  These were as follow:

1. Total quantity of all votes cast for all candidates
2. Total votes cast from within each county, given as absolute quantity and as percentage of all votes across all counties
3. County with greatest voter turnout as determined by total vote quantity
4. Total votes cast for each candidate, given as absolute quantity and as percentage of all votes across all candidates
5. Winning candidate as determined by total vote quantity (given as absolute quantity and as percentage of all votes across all candidates)

The final output of these analyses is included below:
---
Election Results
-------------------------
Total Votes: 369,711
-------------------------

County Votes:
Jefferson:  10.5% (38,855)
Denver:  82.8% (306,055)
Arapahoe:  6.7% (24,801)

-------------------------
Largest County Turnout: Denver
-------------------------

Charles Casper Stockham: 23.0% (85,213)
Diana DeGette: 73.8% (272,892)
Raymon Anthony Doane: 3.1% (11,606)

-------------------------
Winner: Diana DeGette
Winning Vote Count: 272,892
Winning Percentage: 73.8%
-------------------------
---


### Background
Prior to this version of the project program, a simpler version of the script was created which returned only the results listed in the above paragraph as items 1., 4., and 5.  This was deemed insufficient and a new version of the script was written which was able to provide the additional analyses listed above.     

## Results

## Summary