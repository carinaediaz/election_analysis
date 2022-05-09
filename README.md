# Election Analysis

## Overview
##### Assisting the Colorado Board of Elections analyze the election results of three counties to help them certify the votes and determine the winning candidate. 

## Resources
##### Our source of data was the election_results.csv file that contained all the votes cast organized by ballot ID. To automate the process of analyzing this data, we used Python version 3.7.6 and Visual Studio Code version 1.67. 

## Results
##### Tasked with certifying the votes, we were asked to present the Colorado Board of Elections with the total vote count, a breakdown of votes cast per candidate, and voter turnout per county. See the image of the election_analysis.txt file we created with the election results below. 
![election_analysis_results.png]()

## Summary
##### By automating the process of calculating the results for the Colorado Board of Elections, we are able to apply the process to future elections with very few edits. By creating lists and dictionaries that search for the unique occurences of candidate and county names, we avoid manually combing through the data to enter the list options and manually having to edit them if the data changes. See the code selections below that show the creation of the litss and dictionaries and then the for loop that searches for if the candidate does not match any existing candidate names it adds it to the candidate list. The same was done to create the county list. We could easily apply this code to another election csv file that is formatted as the election_analysis.csv with ballot ID in the first column [0], county in the second column [1], and candidate name in the third column [2], the code will be able to calcualte the same results as shown above in the election_analysis_results.png. 

```
# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_list = []
county_votes = {}
```
```
# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)
    # Read the header
    header = next(reader)
    # For each row in the CSV file.
    for row in reader:
        # Add to the total vote count
        total_votes = total_votes + 1
        # Get the candidate name from each row.
        candidate_name = row[2]
        # 3: Extract the county name from each row.
        county_name = row[1]
        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:
            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)
            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0
        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
```

##### Similarly, we also automated the printing of the election results, both in the terminal and in the election_analysis.txt file so that we would not have to manually enter them. By using references to variables we created earlier in the code, you will see in the print command below that if we were to change the data to show that a candidate other than Diana DeGette received the majority vote, their name would appear as the winning candidate automatically.  

```
    # Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)
    # Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
```

##### If the data set were to have additional columns of data that needs to be analyzed, such as a vote on a county proposition, we could easily define the new variables and create commands similar to those we created for the county and candidate vote counts to calculate the results. Created commands with detailed comments makes it much easier to go back and edit or copy old code. 

## Conclusion
##### Through our analysis of the election_results.csv, we were able to conclude and certify that Diana DeGette was the winning candidate, with 272,892 or 73.8% of the votes. Not only were we able to come to this conclusion through the automization of this process with Python code, but this code could easily be applied to future elections with minor edits as needed. 
