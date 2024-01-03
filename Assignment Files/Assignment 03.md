

This grep’s - into anything ending in data (*data), giving the *data file first getting you dates,


grep 'AM\|PM' *schedule | awk -F'[_:"\t" ]' '{print $1 "\t" $4, $5, $7, "\t" $10, $11}' 
This is just RTN (roulette time n name)

grep -f ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Player_Analysis/Notes_Player_Analysis RTN







TEST:

awk '/Billy|Katey/{print $0}' 


# This should let me enter a date and time to show a name.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

if ($date == $1); then grep $1 '~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/RTN'

else
echo "No loss detected for this date." 
fi 







# This should let me enter a date and time to show a name.

echo "Enter the date (MMDD), the time (01-12), either (AM) or (PM), followed each by [enter]:"

read date | read hour | read ampm

grep $date\|$hour\|$ampm RTN 
(doesnt work)





# This should let me enter a date and time to show a name.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

echo "Enter the time (01-12), followed by [enter]:"

read hour

echo "Enter AM or PM, followed by [enter]:"

read ampm

then
grep $date\|$hour\|$ampm RTN



# This should let me enter a date and time to show a name.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

echo "Enter the time (01-12), followed by [enter]:"

read hour

echo "Enter AM or PM, followed by [enter]:"

read ampm

then
grep $date\|$hour\|$ampm RTN



WORKING SCRIPT:
#!/bin/bash
# This should let me enter a date and time to show a name.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date RTN >> MACRO |

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour MACRO >> MICRO |

echo "Enter AM or PM, followed by [enter]:"

read xm

grep $xm MICRO | awk -F" " '{print $3, $4}'

echo "...was the Roulette dealer on:" $date $hour$xm













FINAL ANSWER:

#!/bin/bash
# This should allow you to search the date and time, and give you the corresponding Roulette dealer.

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date RTN | awk -F'["\t" ]' '{print $2, $4, $5, $6, $7}' > MACRO |

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour MACRO | awk -F'["\t" ]' '{print $2, $3, $4, $5}' > MICRO |

echo "Enter AM or PM, followed by [enter]:"

read xm

grep -i $xm MICRO | awk -F'["\t" ]' '{print $2, $3, $4}' 

echo "...was the Roulette dealer on" $date "at" $hour $xm






Using:
grep -f ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Player_Analysis/Notes_Player_Analysis ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/RTN 
I was able to cross reference all the times losses occured during 3/10, 3/11, and 3/12 with corresponding Roulette dealer schedules, highlighting the 13 times losses occured within the dealers schedules, leading to Billy Jones being in cahoots with Mylie Schmidt to scam Lucky Duck.



BONUS:

#!/bin/bash
# This should allow you to search the date and time, and give you the corresponding table dealer.

echo "Enter 1 for Black Jack, 2 for Roulette, 3 for Texas Hold'Em, followed by [enter]:"

read game

grep 0 ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/DS$game > AB |

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date AB | awk -F'["\t" ]' '{print $2, $3, $4, $5, $6, $7, $8}' > CD |

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour CD | awk -F'["\t" ]' '{print $3, $4, $5, $6}' > EF |

echo "Enter AM or PM, followed by [enter]:"

read xm

grep -i $xm EF | awk -F'["\t" ]' '{print $2, $3}'

echo "...was the table dealer on" $date "at" $hour $xm

Term stuff
grep 'AM\|PM' *schedule

awk -F'[_:"\t" ]' '{print $1 "\t" $4, $5, $7, "\t" $8, $9, $10, $11, $12, $13}'   



#!/bin/bash
# This should allow you to search the date and time, and give you the corresponding table dealer.

echo "Enter 1 for Black Jack, 2 for Roulette, 3 for Texas Hold'Em, followed by [enter]:"

read game

grep 0 ~/Lucky_Duck_Investigation/Roulette_Loss_Investigation/Dealer_Analysis/DS$game

echo "Enter the date in MMDD format, followed by [enter]:"

read date

grep $date

echo "Enter the time (01-12), followed by [enter]:"

read hour

grep $hour

echo "Enter AM or PM, followed by [enter]:"

read xm

grep -i

echo "...was the table dealer on" $date "at" $hour $xm



