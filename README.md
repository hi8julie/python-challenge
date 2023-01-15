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



    
