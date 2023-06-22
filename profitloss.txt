import os
import csv

# Path to collect data from the Resources folder
budget_data_csv = os.path.join('Resources', 'budget_data.csv')

#define month as an empty list
months = []
#define profit_loss as an empty list
profit_loss = []
#define change as an empty list
changes = []

# Read in the CSV file
with open(budget_data_csv, 'r') as csvfile:
    # Split the data on commas
    csvreader = csv.reader(csvfile, delimiter=',')

    # Skip the header row 
    next(csvreader)

    #add the month and profit loss
    for row in csvreader:
        months.append(row[0])
        profit_loss.append(int(row[1]))

# Total number of months can be calculated by doing the following
total_months = len(months)

# net_total of months can be calculated by doing the following
net_total = sum(profit_loss)

# The changes in "Profit/Loss" over the entire period can be calculated by doing following
for i in range(1, total_months):
    change = profit_loss[i] - profit_loss[i-1]
    changes.append(change)

# Average of changes in "Profit/Losses calucated by doing following
average_change = sum(changes)/len(changes)

# Greatest increase in profits over the entire period calculated by doing following
Greatest_increase_amount = max(changes)
increase_index = changes.index(Greatest_increase_amount)
Greatest_increase_month = months[increase_index]

# Greatest Decrease in profits over the entire period calculated by doing following
Greatest_decrease_amount = min(changes)
Decrease_index = changes.index(Greatest_decrease_amount)
Greatest_decrease_month = months[Decrease_index]

# Print the results of the analysis 
print("Financial Analysis")
print("------------------------------------------")
print(f"Total Months: {total_months}")
print(f"Total: ${net_total}")
print(f"Average Change: ${average_change:.2f}")
print(f"Greatest Increase in Profits: {Greatest_increase_month} (${Greatest_increase_amount})")
print(f"Greatest Decrease in Profits: {Greatest_decrease_month} (${Greatest_decrease_amount})")
