# Election_Analysis

##Purpose
The purpose of this analysis is to compile the votes for an election, and perform an audit of the results. We will determine the winner of the election, as well as the county with the highest turnout of voters. 

###The Analysis
By pulling in the results from a CSV file we are able to loop through the data and pull each candidate name, the votes assigned to that candidate, and which county the votes came from. 

In this section of code we pull in the CSV and create the text file we will be outputting the results to. 


import csv
import os

# Add a variable to load a file from a path.
file_to_load = os.path.join("Resources", "election_results.csv")
# Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")


For the next part we will read the CSV, and utilize for loops and if statements to compile our data. The for loops will run through the data while the if statements are used to collect the votes and help determine the winners. 




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
        county = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county not in counties:

            # 4b: Add the existing county to the list of counties.
            counties.append(county)

            # 4c: Begin tracking the county's vote count.
            county_votes[county] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county] +=1

Once this is complete we will do similar steps to determine the candidate who won as well. 
        
   ###Final Steps    
    Our final steps are to determine the winners and output them to the text file we created.   
        
        # 7: Print the county with the largest turnout to the terminal.
    winning_county_summary = (
         f"-------------------------\n"
         f"Largest County Turnout: {highest_turnout}\n"
         f"Largest Vote Count: {highest_count:,}\n"
         f"Winning Percentage: {highest_county_percentage:.1f}%\n"
         f"-------------------------\n")
                    
    print(winning_county_summary)

                # 8: Save the county with the largest turnout to a text file.
    txt_file.write(winning_county_summary)

                # Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

         # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

     # Print each candidate's voter count and percentage to the
     # terminal.
    print(candidate_results)
    #  Save the candidate results to our text file.
    txt_file.write(candidate_results)

     # Determine winning vote count, winning percentage, and candidate.
    if (votes > winning_count) and (vote_percentage > winning_percentage):
     winning_count = votes
     winning_candidate = candidate_name
     winning_percentage = vote_percentage

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
    
    
  ###Challenges
  There are many challenges in a program like this. When you pull data from the CSV you must be sure to open the file to allow the program to read through and collect data. Another challenge was correctly indenting the data so that the program reads the code correctly. 
  
  ###Outcome
  
  We see through the course of this challenge that there are multiple factors that can impact the results. Indentation, correct usage of our variables, correctly opening and closing our source file. These all can change the outcomes of our program. 
