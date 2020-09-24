# Election Analysis

## Overview of Election Audit
An employee from the Colorado Board of Elections requested an election audit in tabular results for a US congressional precinct in Colorado to certify the results of the election.  The employee specifically asked for the following data:

&nbsp; &nbsp; 1.) Total number of votes cast<br />
&nbsp; &nbsp; 2.) Total number of votes each candidate received<br />
&nbsp; &nbsp; 3.) Percentage of votes each candidate won<br />
&nbsp; &nbsp; 4.) Winner of the election based on popular vote<br />
&nbsp; &nbsp; 5.) Voter turnout for each county<br />
&nbsp; &nbsp; 6.) Percentage of votes from each county<br />
&nbsp; &nbsp; 7.) County with the highest turnout

## Resources
- Data source: election_results.csv
- Software: Python 3.7, Visual Studio Code version 1.49.1

## Election Audit Results
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

## Explanation of Analysis
The total number of votes was determined with a simple code that looped through each row of the data and increased the total_votes by 1 for each row.
<table>
 <tr>
 <th>Code</th>
 <th>Text File</th>
 <tr>
  <td>
   <pre>
   
  ```py
 for row in reader:
     total_votes = total_votes + 1
  ```
</pre>
</td>
<td>
 
 ![Total Votes](https://github.com/whitneylosinski/Election-Analysis/blob/master/analysis/Total%20Votes.png)
 </td>
</tr>
</table>
 
To determine the results by county, while looping through each row in the data, a list was created by pulling the name of each county that voted in the election from the first index (`row[1]`) in the data, looking to see if it was already in the list, and adding it to the list if it was not already present.  A dictionary was then created to initialize the votes for each county in the list to zero.  Outside of the if statement, the votes were tallied by looking at the county name for each row and adding one vote to the corresponding value in the dictionary each time the county name matched.  
 ```py
  for row in reader:
      # Extract the county name from each row
      county_name = row[1]
      
      if county_name not in county_options:
          # Add the county name to the county options list
          county_options.append(county_name)
          # Set the votes to 0 for each county name
          county_votes[county_name] = 0
      # Add a vote to the corresponding county's vote count.
      county_votes[county_name] += 1
  ```
Once the data was gathered and tallied, the output values were pulled from the data, a calculation was completed to determine the percentage of the total votes that came from each county, and the outputs were written to the Election Analysis text file.
 <table>
 <tr>
 <th>Code</th>
 <th>Text File</th>
 <tr>
  <td>
   <pre>
   
   ```py
   for county_name in county_votes:
        # Retrieve the county vote count.
        county_vote_count = county_votes.get(county_name)
        # Calculate the percent of total votes for the county.
        county_vote_percentage = float(county_vote_count) / float(total_votes) * 100
        # Print the county results to the terminal.
        county_results = (f"{county_name}: 
             {county_vote_percentage:.1f}% ({county_vote_count:,})\n")
        print(county_results)
        # Save the county votes to the text file.
        txt_file.write(county_results)
   ```
  </pre>
</td>
<td>
 
 ![County Results](https://github.com/whitneylosinski/Election-Analysis/blob/master/analysis/County%20Results.png)
 </td>
</tr>
</table>

To determine the county with the largest number of votes, a nested if statement was written to evaluate if the `county_vote_count` was larger than the `winning_turnout` when looping through each county name in the `county_votes` dictionary.  The largest `county_vote_count` was then set as the `winning_turnout`, with the corresponding county name set as the `winning_county`.  The results were then printed and written to the text file.
<table>
 <tr>
 <th>Code</th>
 <th>Text File</th>
 <tr>
  <td>
   <pre>
   
   ```py
   for county_name in county_votes:
       # Determine the winning county and get its vote count.
       if (county_vote_count > winning_turnout):
           winning_turnout = county_vote_count
           winning_county = county_name

   # Print the county with the largest turnout to the terminal.
   winning_county_summary = (
       f"\n-------------------------\n"
       f"Highest County Turnout: {winning_county}\n"
       f"-------------------------\n")
   print(winning_county_summary)

   # Save the county with the largest turnout to a text file.
   txt_file.write(winning_county_summary)
   ```
  </pre>
</td>
<td>
 
 ![Winning County](https://github.com/whitneylosinski/Election-Analysis/blob/master/analysis/Winning%20County.png)
 </td>
</tr>
</table>

The candiate results were determined using very similar code to what was used to determine the county results.  The only difference in the code is that instead of extracting the county name from `row[1]` in the data, the candidate name is now extracted from `row[2]` of the data.  The winning candidate was then determined by using an if statement to see if `votes` was larger than the `winning_count` and the `vote_percentage` was larger than the `winning_percentage` when looping through each candidate name in the `candidate_votes` dictionary.  The largest `votes` was then set as the `winning_count`, the corresponding candidate name set as the `winning_candidate` and the `vote_percentage` was set as the `winning_percentage`.  The results were then printed and written to the text file.
<table>
<tr>
 <th>Code</th>
 <th>Text File</th>
 <tr>
  <td>
   <pre>
   
   ```py
   for candidate_name in candidate_votes:
       # Determine the winning candidate, vote count and vote percentage.
       if (votes > winning_count) and (vote_percentage > winning_percentage):
           winning_count = votes
           winning_candidate = candidate_name
           winning_percentage = vote_percentage

   # Print the winning candidate to the terminal.
   winning_county_summary = (
       f"\n-------------------------\n"
       f"Highest County Turnout: {winning_county}\n"
       f"-------------------------\n")
   print(winning_county_summary)

   # Save the winning candidate to a text file.
   txt_file.write(winning_county_summary)
   ```
  </pre>
</td>
<td>

 ![Candidate Results](https://github.com/whitneylosinski/Election-Analysis/blob/master/analysis/Candidate%20Results.png)
 </td>
</tr>
</table>

## Election Audit Summary

The python script used for this election analysis was able to provide the desired outcomes requested for the audit of this congressional precinct.  However, this script could also be used, with some modifications, for any election.  For example, with additional data, the script could be modified to calculate the winners of several elections at one time.  Since many election ballots consist of multiple elections happening at the same time, the script could be modified to analyze each of the elections on the ballot and provide the results of each election.   Other possible modifications could be made to gain more insight into the ethnicity, age, gender, etc. of the voters who voted for each candidate.  This information could be useful for future election campaigns.
