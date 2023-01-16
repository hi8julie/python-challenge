# python-challenge
# PyBank

#dependencies 

    import os
    import csv 

#defining the path to the csv file in our current directory

    csvpath = os.path.join("Resources/budget_data.csv")

#lists to store data

    months = []
    total_profits_losses = []
    change_profits_losses = []

#opening the csv file 

    with open(csvpath, 'r') as csvfile:
      csvreader = csv.reader(csvfile, delimiter =',')

#read the header row first 

    csv_header = next(csvreader)
   
#iterate through the rows to 1) count number of months 2) add total losses & profits to the list to summarize them later

    for row in csvreader: 
        months.append(row[0])
        total_profits_losses.append(int(row[1]))
        
#iterating through all rows in the Profits/Losses column to calculate the change 

     for x in range(len(total_profits_losses)-1):
        change_profits_losses.append(total_profits_losses[x+1]-total_profits_losses[x])

#looking for the biggest and smallest change (using min and max functions)

    greatest_increase = max(change_profits_losses)
    greatest_decrease = min(change_profits_losses)

#looking for the date associated with the biggest and smallest changes (adding 1 because python starts counting from 0)

    month_increase = change_profits_losses.index(max(change_profits_losses))+1
    month_decrease = change_profits_losses.index(min(change_profits_losses))+1

#printing out the report 

    print("Financial Analysis")
    print("-------------------------")
    print(f"Total Months: {len(months)}")
    print(f"Total: ${sum(total_profits_losses)}")
    print(f"Average Change: ${round(sum(change_profits_losses)/len(change_profits_losses),2)}")
    print(f"Greatest Increase in Profits: {months[month_increase]} (${(str(greatest_increase))})")
    print(f"Greatest Decrease in Profits: {months[month_decrease]} (${(str(greatest_decrease))})")

#defining the path to the text file (report)

    analysis = os.path.join("Analysis/analysis.txt")

#open the analysis file, write the ouput, each line will start with a new line '\n' 

    with open(analysis, "w") as textfile:
      textfile.write("Financial Analysis\n")
      textfile.write("-------------------------\n")
      textfile.write(f"Total Months: {len(months)}\n")
      textfile.write(f"Total: ${sum(total_profits_losses)}\n")
      textfile.write(f"Average Change: ${round(sum(change_profits_losses)/len(change_profits_losses),2)}\n")
      textfile.write(f"Greatest Increase in Profits: {months[month_increase]} (${(str(greatest_increase))})\n")
      textfile.write(f"Greatest Decrease in Profits: {months[month_decrease]} (${(str(greatest_decrease))})\n")

#  PyPoll 

#dependencies 
    
        import os
        import csv 

#defining the path to the csv file in our current directory

        csvpath = os.path.join("Resources/election_data.csv")

#lists to store data

        votes = 0
        unique_candidates = []
        candidates_votes = {}
        vote_percent = []
        winner = []
        votes_per_candidate = []

#opening the csv file 

        with open(csvpath, 'r') as csvfile:
            csvreader = csv.reader(csvfile, delimiter =',')

#read the header row first 

        csv_header = next(csvreader)

#iterate through the rows to count total number of votes

        for row in csvreader: 
            votes += 1
            
#creating a dictionary with names of candidates and their votes

            if row[2] in candidates_votes.keys():
                candidates_votes[row[2]] += 1
            else: 
                candidates_votes[row[2]] = 1
                
#taking values from the dictionary and sorting them as candidates and votes

        for key, value in candidates_votes.items():
            unique_candidates.append(key)
            votes_per_candidate.append(value)

        for x in votes_per_candidate:
            vote_percent.append(round(x/votes*100, 3))

#combining all data into a zip file

        final_report = list(zip(unique_candidates, vote_percent, votes_per_candidate))
        winner_votes = max(votes_per_candidate) 
        winner = unique_candidates[votes_per_candidate.index(winner_votes)]
    
#a different way to find unique values, I defined 'name' as row[2]

        #if name not in unique_candidates:
            #unique_candidates.append(name)
            #candidates_votes[name] = 1
        #else:
            #candidates_votes[name] += 1 
            
#breaking down the list of unique candidates to get the values

    #candidate1_name = str(unique_candidates[0])
    #candidate2_name = str(unique_candidates[1])
    #candidate3_name = str(unique_candidates[2])

    
#printing out the report 

        print("Election Results")
        print("-------------------------")
        print(f"Total Votes:" + str(votes))
        print("-------------------------")
        for candidate in final_report:
            print(candidate[0] + ": " + str(candidate[1]) +'%  (' + str(candidate[2]) + ')\n')
        print("-------------------------")
        print(f"Winner: " + str(winner))
        print("-------------------------")

#I tried to print out the report in a different way but couldn't count % and get a winner with the  defined values. 

        #print(f'{candidate1_name} : ({candidates_votes[candidate1_name]})')
        #print(f'{candidate2_name} : ({candidates_votes[candidate2_name]})')
        #print(f'{candidate3_name} : ({candidates_votes[candidate3_name]})')
        #print(winner)


#defining the path to the text file (report)

        analysis = os.path.join("Analysis/analysis.txt")

#open the analysis file, write the ouput, each line will start with a new line '\n' 

        with open(analysis, "w") as textfile:
            textfile.write("Election Results\n")
            textfile.write("-------------------------\n")
            textfile.write(f"Total Votes: {str(votes)}\n")
            textfile.write("-------------------------\n")
            for candidate in final_report:
                textfile.write(candidate[0] + ": " + str(candidate[1]) +'%  (' + str(candidate[2]) + ')\n')
            textfile.write("-------------------------\n")
            textfile.write(f"Winner: {str(winner)}\n")
            textfile.write("-------------------------\n")


    
