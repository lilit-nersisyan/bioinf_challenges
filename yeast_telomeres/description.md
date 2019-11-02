# Overview
The goal of the yeast telomeres (YT) challenge is to classify strings of given length into two categories: telomeric and non-telomeric. 

The strings have the following characteristics: 
- They have defined length (from 75 to 300, but constant for the given case). 
- They are derived from the dictionary {A,G,C,T,N}. 


The rules defining a telomeric string are:  
- They largely consist of telomeric motifs 
- A telomeric motif is defined by the rule: (TG){1,7}GGTGTG(G)?
- The beginning of the string may lack telomeric motifs 
- With small frequency, the motifs may be separated by one-two letters
- The motifs may have errors: substitution (replacement of one character with another from the dictionary {A,G,C,T,N}), insertion (a novel character in-between motif characters) or deletion (removal of one character)

## Example
For example: the following string is a telomeric one. 
TGTGTGTGGGTGTGGTGTGTGTGTGTGTGGGTGTGGTGTGTGTGTGGGTGTGGGTGTGGTGTGTGTGT 

Below is the break-up of the string. The motifs parts are defined within round brackets, while the errors are in blue: 

<pre>
{(TGTGTGTG)(GGTGTG)(G)} {(TGTGTGTGTGTGTG)(GGTGTG)(G)} {(TGTGTGTGTG)(GGTGTG)(G)} <span style="color:red">[G]</span> {(TGTG[G]TGTGTGTGT)...}
</pre>

Other strings may appear to be half-telomeric, with the telomeric part starting after several characters: 
TAGGGTAGTGTTAGGGTAGTGTTAGGGTAGTGTGGTGTGGTGTGTGGGTGTGGGTGTGGGTGTGTGTGTGGGTGTGGTGTGTGGGTGTGGTGTGTGGGT
<pre>
[TAGGGTAGTGTTAGGGTAGTGTTAGGGTAG]{(TGTG)(G[-]TGTG)(G)} {(TGTGTG)(GGTGTG)(G)} [G] {(TGTG)(GGTGTG)} {(TGTGTG)(GGTGTG)(G)} {(TGTGTG)(GGTGTG)(G)} {(TGTGTG) (GGT)...}
</pre>

## Challenge question
Given a set of telomeric and non-telomeric strings, determine the nature of the strings and submit the number of telomeric strings as your answer. 

## Challenge data
Several datasets, with varying numbers of telomeric and non-telomeric strings and with different lengths and error-rates will be provided. The number of strings in each dataset will be on the order of 1M. 
The true number of telomeric strings will be known a priory. The adjusted R squared value of correlation between known and predicted numbers will be used for estimating the accuracy. 
This is a competitive challenge: the accuracy of submissions will be used to determine the winning solution. 

## Timeline

# Biology: where is this applicable? 
