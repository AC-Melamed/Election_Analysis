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


### Background
Prior to this version of the project program, a simpler version of the script was created which returned only the results listed in the above paragraph as items 1., 4., and 5.  This was deemed insufficient and a new version of the script was written which was able to provide the additional analyses listed above with additional 'for' loops and conditional statements.     

## Results
The final outputs for this project's analyses are shown below:
```
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
```
A detailed breakdown of the program script used to determine each of the above results is provided below:

#### Total Votes
A unique counter variable is initialized for tracking the total vote quantity
```
total_votes = 0
```
Each row in the .CSV file containing the election data is counted as a discreet vote and tallied into the counter
```
    for row in reader:
        total_votes = total_votes + 1
```
The final quantity is printed and written to the .TXT file
```
with open(file_to_save, "w") as txt_file:

    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)
```
The result returned shows that the total number of votes cast in the election was 369,711.

#### County Votes
A list is created for storing the names of each county as well as a dictionary for storing the names in conjunction with their respective vote counts
```
county_list = []
county_votes = {}
```
The county name for each row is extracted and checked for uniqueness before being added to the list
```
        county_name = row[1]
```
```
        if county_name not in county_list:

            county_list.append(county_name)
```
The number of votes for each county is counted and added to the dictionary
```
            county_votes[county_name] = 0

        county_votes[county_name] += 1
```
Each county and its respective vote count are retreived from the dictionary and calculated as a percentage before being printed and saved to the .TXT file as both percentage and absolute quantity
```
    for county_name in county_votes:
        
        county_votecount = county_votes.get(county_name)

        county_votecount_percentage = float(county_votecount) / float(total_votes) * 100
        
        county_results = (f"{county_name}: {county_votecount_percentage: .1f}% ({county_votecount:,})\n")
        print(county_results)

        txt_file.write(county_results)
```
The results returned show that the citizens of Jefferson county contributed 10.5% of the total vote with 38,855 individual votes, those of Denver county contributed 82.8% with 306,055 votes, and those of Arapahoe county contributed 6.7% with 24,801 votes.

#### Largest County Turnout
The county with the greatest voter turnout is determined by first declaring an empty string, an absolute quantity variable, and a percentage variable
```
largest_county = ""
largest_votes = 0
largest_votes_percentage = 0
```
An 'If' statement is used to compare the vote count for each county and assign the county with the greatest value
```
        if (county_votecount > largest_votes):

            largest_votes = county_votecount
            largest_turnout = county_name
```
This county is then printed and saved to the .TXT file as the one with the largest turnout
```
    largest_turnout_printing = (
        f"\n-------------------------\n"
        f"Largest County Turnout: {largest_turnout}\n"
        f"-------------------------\n\n"
        )
    print(largest_turnout_printing, end="")
```
The result returned show that Denver county was the county with the greatest voter turnout for the election.  

#### Candidate Votes
A list is created for storing the names of each candidate in the election along with a dictionary for storing the names in conjuction with their respective vote counts
```
candidate_options = []
candidate_votes = {}
```
The candidate names are read from the .CSV file, checked for uniqueness, and added to the list
```
        candidate_name = row[2]
```
```
 if candidate_name not in candidate_options:

            candidate_options.append(candidate_name)
```
The votes corresponding to each candidate name are counted and added to the dictionary
```
            candidate_votes[candidate_name] = 0

        candidate_votes[candidate_name] += 1
```        
The final vote quantities for each candidate are retreived from the dictionary and calculated as percentages of the total vote before being printed and saved to .TXT file as such
```
    for candidate_name in candidate_votes:

        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        print(candidate_results)
        txt_file.write(candidate_results)
```
The results returned show that Charles Casper Stockham received 23.0% of the vote with 85,213 total votes, Diana DeGette received 73.8% with 272,892 votes, and Raymon Anthony Doane received 3.1% with 11,606 votes.

#### Winning Candidate
To determine the candidate projected to have won the election based on popular vote, an empty string and two variables are first declared
```
winning_candidate = ""
winning_count = 0
winning_percentage = 0
```
Using the vote counts and percentages previously calculated for each candidate, the greatest quantities for both are identified along with their corresponding candidate name
```
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
```
The candidate determined thus to have received the majority of the total vote is then printed with the absolute quantity and percentage of the total vote received and saved to the .TXT file as the winner of the election.
```
    winning_candidate_summary = (
        f"\n-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

    txt_file.write(winning_candidate_summary)
```
The result returned here shows that Diana DeGette is the projected winner of the election, having received 73.8% of the total vote with 272,892 invidual votes.

## Summary
As a whole, the script used for this project appears emminantly applicable across many other potential election data corpora.  The framework of the analyses performed therein is not hardcoded to any of the dimensions of the dataset used in this case; only the content of the particular rows in the .CSV are directly referenced.  

Imagining other such potential applications, two broad modifications to the script might be proposed:

#### National Elections
In the case where a national election has taken place and the voting data is provided in the form of multiple .CSV files such as the one provided for this project, indexed by candidate and county, the existing script could be modified using Pandas to read each file into a list of separate dataframes.  The existing analyses could then be performed on each dataframe, representing each state's voting results, which could even be weighed according to electoral college rules as necessary before being recompiled into a final national dataframe for a final round of analysis to determine the national results.

#### Visualizations
While the results for this project are concise and easily parsed, elections with more numerous candidates or counties at play might benefit from data visualizations.  By using Matplotlib, Pyplot, and Numpy, the existing dictionaries in this project's script could be easily used to generate a variety of different useful charts.  For instance, pie charts are often used in the case of elections to show the vote distribution across candidates.   
