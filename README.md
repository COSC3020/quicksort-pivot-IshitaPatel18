[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/IF3rQO50)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

My answer:

On slide 34, it is dicussed that for the average case, there is a 1/4 chance of getting
a pivot that is less than the good n/2 elements and there is a 1/4 chance of getting
a pivot that is greater than the good n/2 elements. So if were to choose the first element
we have an equal chance of getting a good pivot as it is 1/2 or 50% chance and then 1/4 or 25%
for each side of the good pivot, making a "bad pivot" choice also 50%. 

Now if we were to use the median-of-three approach we have to determine all the possibilities
of the first, middle, and last elements on the spectrum of good and bad pivots. For the elements 
that are less than the ideal n/2 pivot range, they will be labeled as "L", the elements that are
greater than the ideal n/2 pivot range will be labeled as "G", and the elements that fall perfectly
into the pivot range will be labeled as "P", in the calculations. Now these are all the possible 
combinations of what each first,middle,and last element chosen can be: (LLL) (LLP) (LPL) (PLL)
(LPG) (PGL) (GLP) (LGP) (PLG) (GPL) (PPP) (PPL) (PLP) (LPP) (PPG) (PGP) (GPP) (GGG) (GLL) (LGL)
(LLG) (GGP) (GPG) (PGG) (GGL) (GLG) (LGG). These can be simplified into categories for easier
computation: 1(LLL) 1(PPP) 1(GGG) 3(LLP) 6(LPG) 3(PPL) 3(PPG) 3(LLG) 3(GGP) 3(GGL).

Now we can calculate the probability of each of the combinations based on their probability
from the pivot spectrum from slide 34 and in the quantity that they occur:
LLL = $(1/4)^3 * 1 = 1/64$
PPP = $(1/2)^3 * 1 = 8/64$ or 1/8
GGG = $(1/4)^3 * 1 = 1/64$
LLP = $(1/4)^2 * 1/2 * 3 = 6/64$ or 3/32
LPG = $(1/4)^2 * 1/2 * 6 = 12/64$ or 6/32
PPL = $(1/2)^2 * 1/4 * 3 = 12/64$ or 3/16
PPG = $(1/2)^2 * 1/4 * 3 = 12/64$ or 3/16
LLG = $(1/4)^3 * 3 = 3/64$
GGP = $(1/4)^2 * 1/2 * 3 = 6/64$ or 3/32
GGL = $(1/4)^3 * 3 = 3/64$

Now, we know that the median strategy is going to choose the middle element, because 
the median is found by removing one element from the low end and one element from the 
high end one at a time from a sorted list(in this case a sorted list of 3 elements) 
until the middle element is found. With that knowledge in mind, we can eliminate any 
scenarios where P wouldn't be the middle element. This removes, LLL, GGG, LLP, LLG, 
GGP, and GGL as they either don't contain P, or P would not be the middle element.
Now if we add the probability of all the remaining scenarios that would give us P as 
the middle element (PPP + LPG + PPL + PPG = 8/64 + 12/64 + 12/64 + 12/64) we would
have 44/64 or 68.75% chance of choosing a good pivot using the median-of-three strategy.
Comparing this to our leftmost element as a pivot approach, we get a 50% chance of having
a good pivot, but with the median-of-three strategy we get 68.75% which is better. So
the median-of-three approach is a better method of choosing a pivot than simply 
choosing the first element!

