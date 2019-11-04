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

Below is the break-down of the string. The motifs are defined within curly brackets, the motif-parts - within round brackets, while the errors are in square brackets: 

<pre>
{(TGTGTGTG)(GGTGTG)(G)} {(TGTGTGTGTGTGTG)(GGTGTG)(G)} {(TGTGTGTGTG)(GGTGTG)(G)} [G]{(TGTG[G]TGTGTGTGT)...}
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

# Biology: why is this interesting?

## What are telomeres?
Every living cell has a DNA. The DNA is a long double-stranded chain of four different types of molecules (nucleotides or bases) denoted as A, G, C or T, which store the genetic information. In each cell the DNA is fragmented into a few fragments, each of them called a chromosome. Human cells, for example, each have 23 pairs of chromosomes. The middle parts of each linear chromosome contain information that is used by the cell to produce anything it needs for performing its everyday tasks. The ending parts, however, do not explicitly store useful information, but have a peculiar structure: the telomeres. 

The cell always repairs itself, and most importantly its DNA. If the chromosomes breaks into peaces, say under UV radiation, the cell immediately senses the breaks and glues them back together. The linear chromosomes, however also start and end with breaks and they need to find a way to conceal themselves from this repair process. This is where the telomeres step in. The starting and ending regions of the linear chromosomes are called telomeres and have a specific sequence of bases, which allows them to form knot-like structures. The knot is formed becasue one of the telomeric strands is longer than the other and it folds back onto the short one, thus forming a knot and saving the chromosome endpoints from being recognized as breaks.  

![telomeres versus DNA sticky ends](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/telomeres_vs_sticky_ends.png)

This elegant solution to the chromosome endpoint problem, however, leads to yet another peculiarity of telomeres: they get shorter as we age. Our aging process is accompanied by continues division of our cells. When the cell wants to divide, it first replicates its DNA: makes two copies of each of the original strands. Importantly, after making a copy, one of the strands is cut to make it shorter than the other, so that the telomeric knot can be formed. This, however, means that after each round of DNA replication, the telomeres will be cut and will become shorter and shorter. What happens when telomeres get extremely short? The cell stops dividing. And when the cells stop dividing, the tissues and organs loose the ability to repair themselves. This is what happens in the organisms of older people. 

![the structure of telomeres](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/telomeres_structure.png)

### How long are the telomeres? 
The sequence of human chromosomes is built up of consecutive repeats of the form: TTAGGG. These repeats concatenated in one telomeric region may span around 10.000 bases. For your comparison, all the human chromosomes together contain around 3bln bases of DNA. 

## Telomeres and human diseases 

As you may guess, telomere shortening is one of the factors responsible for aging. Not surprisingly, they are also associated with age-related diseases, such as cardiovascular diseases and premature aging syndrome (Robin Williams stars a guy that suffers from such a disease in the [movie Jack](https://www.imdb.com/title/tt0116669/?ref_=fn_al_tt_1)). Smoke, and you'll run the danger of making your telomeres shorter, thus increasing your risk of getting these disorders. 

What about cancers? We know that tumors are formed by uncontrolled division of cells. Tumors know no limits: they may grow indefinitely, with cells dividing over and over again. How is this possible? Well, one of the factors that cancer cells have to take care of are telomeres. It appears, cancer cells know how to make their telomeres longer, thus being able to divide as many times as needed. Consequently, there are multiple medications and therapies targetted at telomeres. Those try to stop the process of telomere elongation in cancer cells thus controlling tumor growth. 

## Yeast telomeres
Yeast are unicellular fungi. They are frequently used in baking to make the dough soft and porous. Besides being useful in the kitchen, they are also great model organisms used by biologists in their laboratories. Even though yeast are not similar to us by their looks, the basic molecular events and processes largely resemble those in human cells. Therefore, studying telomeres in yeast will provide clues on how to control telomere length in humans too.

As humans, yeast also have linear chromosomes ending with telomeric regions. The telomeres in yeast, however, have a different repeat pattern. This pattern is not strictly defined, but is a motif of the form: (TG){1,7}GGTGTG(G)?. Concatenate multiple repeats like this, each time choosing to repeat (TG) 1-to-7 times and either adding G at the end or not, and you'll get the sequence of yeast telomeres. 

## How are the telomeres studied? 

Usually, expensive experimental procedures are involved. Most of the techniques involve chemicals that bind to telomeres and emit light, allowing to assess the length of telomeres. These techniques are first of all expensive and time consuming. Secondly, not many labs have performed telomere length measurement during their experiments. Therefore, there is not much data on telomere length coupled with other interesting characteristics. 

On the other hand, people nowadays are talking about the huge amount of genomic (or DNA-sequencing data). These datasets reach petabytes in size and are mostly freely available through public databases. Our aim is to leave the expensive experiments behind and re-use the freely available DNA-sequencing data to study telomeres! 

## DNA sequencing
DNA sequencing is the process of obtaining or reading the sequence of bases in a DNA strand. The second generation of sequencing machines does it by randomly shearing the DNA molecules (of length 75-250 bases on average), and reading those sequences. The readings are called sequencing reads. The main problem of sequencing datasets is that the origin of the reads is no known, so one has to identify their origin by complicated bioiformatics algorithms. Telomeric sequences pose particular problems, as their are of repetitive nature. 
![DNA sequencing and the task](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/sequencing_reads.png)

Your solution will be a real contribution to the field of bioiformatics and telomere biology! Have fun! 

