# Simple Maximum Likelihood Tree Inference Tutorial
===================


## Single gene tree inference.

This tutorial is designed for researchers or students who want to infer a single gene tree using robust methods. This tutorial is not designed to teach phylogenetic theory or background information that users should be aware of before performing phylogenetic inference. 

Gene tree inference has become easier than ever with user-friendly programs like IQ-TREE. I generally think this is a good thing, but researchers should be cautious to use programs if they do not understand the underlying approach. Therefore, I encourage users to read about homology, sequence alignment, substitution models, and other theoretical foundations of molecular phylogenetic infernece. Systematic error and other potential pitfalls that can occur when inferring phylogeneies should also be understood.

### Aligning genes, loci, or orthologous groups.

First, individual genes (or loci, or orthologous groups) should be aligned. I recommend mafft (https://mafft.cbrc.jp/alignment/server/index.html) as a robust tool, but numerous options exist. This tutorial assumes that your genes have already been aligned and that your file of aligned sequences is in fasta or phylip format.

### Partitioning and files needed for IQ-tree

If your gene is not a protein coding gene (e.g., 16S, 28S, ITS), you can skip this section. 

If your gene is a protein coding gene, the different codon positions likely evolve differently. For that reason, best practice is to include partition finding in the tree search. For this, you will need a file that defines starting "blocks" for partition finding. 

Let's assume your gene is 658 bp. That is, the lenght of the standard barcoding gene fragment for mollusks, a partial section of the COI mitochondrial gene. Partition block file format information can be found here: https://iqtree.github.io/doc/Complex-Models#partition-models

An example for COI:   
 
```
DNA, codon1 = 1-658/3
DNA, codon2 = 2-658/3
DNA, codon3 = 3-658/3
```

 
Save that text into a file like partition.txt



### A single iq-tree command

Once you have an alignment and a partition file you can infer a tree with single IQ-TREE command

```{iqtree command with fasta file alignment, echo = T, results = 'hide', error=FALSE, warning=FALSE, message=FALSE}
iqtree3 -s alignment.fas -p partition.txt -B 1000 -pre COI-gene-tree -m MFP+MERGE -T 4
```

or 

```{iqtree command with phylip file alignment, echo = T, results = 'hide', error=FALSE, warning=FALSE, message=FALSE}
iqtree -s alignment.phy -p partition.txt -B 1000 -pre COI-gene-tree -m MFP_MERGE -T 4
```

IQ-Tree will output several files. The maximum likelihood tree, and therefore the tree you should report, is the .treefile. In most cases, you do not want to report the .contree

## Next step
You can now open up the maximum likelihood tree in your favorite visualization program. I like FigTree.
