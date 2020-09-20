# Election Analysis

## Overview of Election Audit
An employee from the Colorado Board of Elections requested an election audit in tabular results for a US congressional precinct in Colorado to certify the results of the election.  The employee specifically asked for the following data:

  1.) Total number of votes cast
  2.) Total number of votes each candidate received
  3.) Percentage of votes each candidate won
  4.) Winner of the election based on popular vote.

## Resources
- Data source: election_results.csv
- Software: Python 3.7, Visual Studio Code version 1.49.1

## Election Audit Results: Use images or examples of your code as support where necessary.
The results of the analysis show that:
 - There were a total of 369, 711 votes cast in this congressional election.
 - The turnout results by county were:
    - Jefferson County: 38,855 voters (10.5%)<br />
    - Denver County: 306,055 voters (82.8%)<br />
    - Arapahoe County: 24,801 voters (6.7%)
 - Denver county registered the largest number of votes.
 - The candidate results were:
    - Charles Casper Stockham: 85,213 votes (23.0%)<br />
    - Diana DeGette: 272,892 votes (73.8%)<br /> 
    - Raymon Anthony Doane: 11,606 votes (3.1%)
 - The winning candidate was Diana DeGette who received 272,892 votes and 73.8% of the popular vote.

## Election Audit Summary

The python script used for this election analysis was able to provide the desired outcomes requested for the audit of this congressional precinct.  However, this script could also be used, with some modifications, for any election.  For example, with additional data, the script could be modified to calculate the winners of several elections at one time.  Since many election ballots consist of multiple elections happening at the same time, the script could be modified to analyze each of the elections on the ballot and provide the results of each election.   Other possible modifications could be made to gain more insight into the ethnicity, age, gender, etc. of the voters who voted for each candidate.  This information could be useful for future election campaigns.
