## Paradiso - 10 points

#### Description: 
N/A

#### Solution: 
For this anomaly, we were given an file titled "attachment" that had the bytecode for a .dis file. Here is what we were able to decifer after using the "strings" command to convert the file to binary:

![[Pasted image 20220215221927.png]]

After plugging in certain parts of the string in CyberChef from hex into string format, we were able to retrieve the flag:

cdc{ Well pleas'd to leave so cruel sea behind; And of that second region will I sing, In which the human spirit from sinful blot Is purg'd, and for ascent to Heaven prepares. }