# Total_Count_IP

This repository contains the answer for this Trailblaze community question: https://trailhead.salesforce.com/pt-BR/trailblazer-community/feed/0D54V00007ermleSAA

## Input/Output of the Integration Procedure:

The input contains a list of values of "location stores," and the output counts the occurrences of these values in the list on the node "location count.".

Example:

![img_1](https://github.com/user-attachments/assets/cb8f0343-2615-48ac-a91b-9abc337f1c9b)


## DataRaptor Transform:

The DataRaptor Transform that receives this input list and outputs only the unique LocationStores of the list:

![dr_transform_output](https://github.com/user-attachments/assets/1059fcae-575c-4938-bbae-26b6b458a3f9)

This was achieved by this formula that trims the unique values of the LocationStores list: 

LIST(LISTMERGE("LocationStore",LIST(%LocationStores%)))

## Integration Procedure:

The integration procedure structure has the DataRaptor Transform and a LoopBlock that iterates over the output from the DataRaptor Transform.

Having a SetValues inside the loopblock with the following formula:

LISTSIZE(FILTER(LIST(%LocationStores%),'LocationStore == "' + %DRTransform_ListToCounts:unicList:LocationStore% + '"'))

This formula will count the size of the LocationStores initial list filtered by the LocationStore that we are iterating; this way we could get the LocationCount of the eatch iteration over the unic list, and inside the loopblock it displays like this:
