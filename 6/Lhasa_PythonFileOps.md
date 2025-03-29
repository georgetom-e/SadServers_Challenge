Description: There's a file /home/admin/scores.txt with two columns (imagine the first number is a counter and the second one is a test score for example).

Find the average (more precisely; the arithmetic mean: sum of numbers divided by how many numbers are there) of the numbers in the second column (find the average score).


Solution: Python Script 


    with open("scores.txt") as file:

    sum=0
    items=0

    for line in file:
        arr=line.split()

        sum+=float(arr[1])

        items+=1

    average=round(total / items, 2)
    
    print(f"Average: {average}")
    
    #Write avergae into file
    
    with open("~/solution", "w") as solution_file:
        solution_file.write(str(average))

