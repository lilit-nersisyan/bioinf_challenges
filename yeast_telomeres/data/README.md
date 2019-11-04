# Data overview

- Three chromosomes (DNA strings) have been used to generate the dataset. Each chromosome contains a string from {A,G,C,T,N} library, on the order or 300.000 in length. 
- Telomeric strings of length from normal distribution (with mean 300 and standard deviation 40) was attached to the two ends of each chromosome. 
- The telomere-containing chromosomes were then randomly sheared into predefined length-fragments, with a default rate of errors introduced by the ART tool. 
- The datasets will be provided in the form of fastq formatted files, which contain the strings (further reffered as reads) to be classified. The format of fastq files is described below. Apart from the read sequences it also contains information on the quality of each base (letter). If the quality is low, it is likely that there's an error at that position. It is up to you to decide whether or not to use the quality information.
- The option "coverage" determines how many times each base in the original chromosome sequence is included in the produced reads. The values 1 and 10 have been used in the provided datasets.
- Your task is to classify the reads into telomeric and non-telomeric ones, and compute their average length with the formula given below.
- The predicted and true values of telomere length (L) will be compared to determine the winner. 


## fastq file format
A fastq file consists of consecutive entries, each entry relating to a specific read. An entry consists of the following four lines: 

<pre>
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
</pre>

The first line always starts with '@' and denotes the read name. 
The second line is the actual read sequence. 
The third line is always '+'. 
The fourth line is the quality of the read bases - each symbol corresponding to a single base in the read above. The byte representing quality runs from 0x21 (lowest quality; '!' in ASCII) to 0x7e (highest quality; '~' in ASCII). Here are the quality value characters in left-to-right increasing order of quality (ASCII):

<pre>
!"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
</pre>

## fastq file names 
Each fastq file has the following naming style: 
"sequencing system"_"read length in (bp)"_"coverage(x)"_"chromosome"@tel1-"length of the first telomeric end"_tel2-"length of the second telomeric end".fq
For example, the following file has been generated with "ns50" sequencing system, contains reads of length 75, generate with 1x coverage from chromosome 3, concatenated with 370 and 245 length telomeric ends: 
ns50_75bp_1x_chr3@tel1-370_tel2-245.fq

## reverse complement 
As already mentioned, the chromosome is concatenated with two telomeric ends. While the second end is built with the consecutive repeats of the form (TG){1,7}GGTGTG(G)?, the first telomeric end is reverse complemented. This means the following: 
- The sequence is reversed: the last base is read the first, the first one the last and so on. 
- The sequence is complemented: each base is replaced with its complement with the following rule: 
A - T
T - A
G - C
C - G 
N - N 
a - t 
t - a 
g - c
c - g 
n - n

For example, the following is a 20bp-long telomeric string. 
<pre>
CACACCCACACACCCACACA
</pre>

It is reverse compelmented from: 
<pre>
TGTGTGGGTGTGTGGGTGTG
</pre>

## telomere length 

- To compute the length of the telomeres in a given dataset, use the following formula: 
<pre>
L = (read_length * num_of_telomeric_reads/coverage) / 2
</pre>
The division by 2 is for taking the average of the two telomeric ends. 

\* Instead of using the number of reads and the read length, one can also calculate the cumualative length of telomeric regions in each read. However, given our experience, there's no need to make things so complex.

- The length of telomeres at the two ends of each chromosome is given in the name of each fastq file. Their average is used as the true L. 
- The solution that leads to least root mean squared error from the original lengths and highest correlation R-square, will win. 
