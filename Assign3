
# Name= Rubaisha Aslam
# Assignment 3
# In this function we would find the list of candidates and sort it from the first to be eliminated to the last
# We will use input, for loop, if statement, dictionary and function
def openIT():
    """
    return: the total data in file as lists in one big list
    """
    # all data [[voter1], [voter2], ..., [voter n]]
    # check the maximum to use in the second function
    max_candidate_num = 0
    finalData = []
    fileData = input("Enter the name of the file: ")
    with open(fileData, 'r') as votesData:
        for line in votesData:
            lineData = line.strip().split(",")
            voter_i = []
            for vote in lineData:
                if vote == " " or vote == '':
                    pass
                else:
                    voter_i.append(int(vote))
                    max_candidate_num = max(max_candidate_num, int(vote))
            finalData.append(voter_i)
    return finalData, max_candidate_num


def calculateValue(finalData):
    """
    param: finalData: the list with all the values
    return: returns the percent in decimals
"""
    # make a dictionary and find the percentage of the IDs (candidates)
    sumOfAll = 0
    dictionaryOfVote = {}
    # for loop to add value in the dictionary
    for voter in finalData:
        if len(voter) != 0:
            firstCandidate = voter[0]
            if firstCandidate not in dictionaryOfVote:
                dictionaryOfVote[firstCandidate] = 1
            else:
                dictionaryOfVote[firstCandidate] = dictionaryOfVote[firstCandidate] + 1
    # find the full sum and than divide to find the percentage
    for item in dictionaryOfVote:
        sumOfAll = dictionaryOfVote[item] + sumOfAll

    for item in dictionaryOfVote:
        dictionaryOfVote[item] = (dictionaryOfVote[item] / sumOfAll)

    return dictionaryOfVote


def calculate_winner(percentValue):
    """
    param: percentValue: it is the percent of the value
    return: returns 0 or the value if its above 50%
    """
    # check winner by seeing the percent if its above 50 return the ID if not return 0
    for ID in percentValue:
        if percentValue[ID] > 0.5:
            return ID

    return 0


def calculate_loser(percentValue):
    """
    param: percentValue: it is the percent of the value
    return: the lowest value
    """
    # checks the minimum value
    min_percentages = float('inf')
    # compare the new ID with the old value and store the lowest one
    for ID_value in percentValue:
        if percentValue[ID_value] < min_percentages:
            min_percentages = percentValue[ID_value]
    # create a list that would be appended with the lowest one
    loser_list = []
    for ID in percentValue:
        if percentValue[ID] == min_percentages:
            loser_list.append(ID)

    realLoser = max(loser_list)

    return realLoser


def delete_loser(all_data, loser):
    """
    param: all_data, loser: so you get the loser value and the file
    return: remove the lowest from file
    """
    # it would compare the values and remove the lowest value from the first list
    for voter in all_data:
        for vote in voter:
            if loser == vote:
                voter.remove(loser)

    return all_data


def main():
    # put together all of the functions and print the elimination order
    finalData, max_candidate_num = openIT()
    goneList = []

    while True:
        percentValue = calculateValue(finalData)
        winner = calculate_winner(percentValue)

        # goes through the whole loop and add to a new list and later appends the winner to the list in order
        if winner != 0:
            other_losers = []
            for i in range(1, max_candidate_num+1):
                if i not in goneList:
                    if i != winner:
                        other_losers.append(i)

            if len(other_losers) > 0:
                other_losers.sort()
                goneList = goneList + other_losers + [winner]
            else:
                goneList = goneList + [winner]
            break

        loser = calculate_loser(percentValue)
        goneList.append(loser)
        finalData = delete_loser(finalData, loser)

    goneString = ", ".join(repr(e) for e in goneList)
    # print order
    print("Elimination order: {}".format(goneString))
    return goneString


main()
