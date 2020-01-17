We are given strings from a library of 20 different characters. These strings correspond to count vectors - each position in a string has a count. 
We then construct count vectors of length 30 for each character, which indicate cumulative counts across the input strings at positions -30 to 0 relative to the character. 
For example, below you see counts for two different characters A and T. The x axis reflects the distance from the character, the y axis is the cumulative count. 
![Count vectors for two characters: A and T](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/count_vectors.jpg)

The problem here is that the A count vector contains a mix from T counts. 

**Toy example (6 positions instead of 30 in the image above)**

If you have two strings and the coressponding count vectors like this:

<pre>
S1: 

string:          ****AT*** 
counts:          114520100
distance from A: 43210
distance from T: 543210

S2: 

string:          **A***T** 
counts:          432141000
distance from A: 210
distance from T: 6543210

</pre> 

Then the summed counts for A and T for the two strings will be: 

<pre>
counts from A:   0011884
distance from A: 6543210

counts from T:   4435930
distance from T: 6543210

</pre>

Now, we assume that each character A and T has their own influence on counts from a certain distance from them. Say, the counts peak for A and T at distance -2 from them.  
However this peak is not visible for A, because of mixture of counts from T. At distances -2 and -1 from A, the counts are equal: 8. In other words, the count at distance -2 from A is not visible, because of the neighboring T, that adds additional counts at the distance -1 from A. 

**A better illustration of the problem**

We usually expect uniform counts for each character: 
![Uniform_counts](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/uniform_counts.jpg)

But when one of the characters (X) drastically influences counts at position -17, then the count vectors for the rest of the characters get biased. It is because counts at -17 for X is are actually counts at, say -14 for A, or at -11 for B, and so on.  

![Biased_counts](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/biased_counts.jpg)

**The task**

The task is vague. Can we somehow deconvolute the final count vectors A (0011884), T (4435930) and the rest 18 characters? 
Say, can we estimate and reduce the influence of T from all the vectors?

