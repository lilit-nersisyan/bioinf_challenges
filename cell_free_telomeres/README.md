## What are telomeres?
In 1961 Leonard Hayflick, a professor at Standford, discovered an interesting phenomenon. He isolated human cells and grew them in a dish, and to his surprise he noticed that the cells wouldn't live forever: they would divide at most 50-60 times and then would stop dividing and die. Even more intriguing was the fact that cancer cells could live forever, with indefinite number of divisions. 

![Leonard Hayflick](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/L_Hayflick.jpeg)

Only ten years after this discovery, it became clear what makes our cells tick. The secret to cellular aging lied in DNA. 

Every living cell has a DNA. The DNA is a long double-stranded chain of four different types of molecules (nucleotides or bases) denoted as A, G, C or T, which store the genetic information. The middle parts of each linear chromosome contain information that is used by the cell to produce anything it needs for performing its everyday tasks. One of these tasks is division and tissue renewal. You loose old skin cells everyday, and those are replaced with new once. If you drink alcohol you loose liver cells, and those are fortunately replaced with new ones. Unfortunately, these renewal processes are declining as we age, with our skin being less elastic, and our liver - less flexible to our habits: all because our cells age and do not divide anymore. Why? 

Because before each division the cell replicates its DNA to deliver two copies to the two daughter cells. Howevver, the cell fails to make copies of the very ends of DNA. Can you imagine what would happen if these ends coded for some essential proteins? Fortunately, the ends of DNA are just stretches of repetitive sequences, called the <i>telomeres</i>. Before each cellular division the tip of the telomeric DNA is lost, and when the telomeres become too short, the cell stops dividing. Telomeres are protecting our DNA like the tips of the shoelaces protect the shoelace from breaking apart.  

![telomere_shortening](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/telomere_shortening.jpg)

What about cancer cells? Well these cells can make their telomeres longer! That is why many drugs are now being developed to shorten cancer telomeres and stop tumor growth. What if a person's telomeres grow too short? Well, this is also a problem: check out the [movie Jack](https://www.imdb.com/title/tt0116669/?ref_=fn_al_tt_1), starring Robin Williams, about guy that suffers from a premature aging syndrome: at his 13 years he looks like 40 years old - all because of problems with telomeres.  

### How long are the telomeres? 
The sequence of human chromosomes is built up of consecutive repeats of the form: TTAGGG. These repeats concatenated in one telomeric region may span around 10.000 bases. For your comparison, all the human DNA altogether contains around 3bln bases of DNA. 

## How are the telomeres studied? 

Usually, expensive experimental procedures are involved. Most of the techniques involve chemicals that bind to telomeres and emit light, allowing to assess the length of telomeres. These techniques are first of all expensive and time consuming. Secondly, not many labs have performed telomere length measurement during their experiments. Therefore, there is not much data on telomere length coupled with other interesting characteristics. 

On the other hand, people nowadays are talking about huge amounts of genomic (or DNA-sequencing data). These datasets reach petabytes in size and are mostly freely available through public databases. Our aim is to leave the expensive experiments behind and re-use the freely available DNA-sequencing data to study telomeres! 

## DNA sequencing
DNA sequencing is the process of obtaining or reading the sequence of bases in a DNA strand. The second generation of sequencing machines does it by randomly shearing the DNA molecules (of length 75-250 bases on average), and reading those sequences. The readings are called sequencing reads. The main problem of sequencing datasets is that the origin of the reads is no known, so one has to identify their origin by complicated bioiformatics algorithms. Telomeric sequences pose particular problems, as they are of repetitive nature. 

The challenge of studying telomeres from DNA sequencing datasets is to distinguish reads derived from the telomeric DNA regions from those coming from the rest of the genome.

![DNA sequencing and the task](https://github.com/lilit-nersisyan/bioinf_challenges/blob/master/figures/sequencing_reads.png)
