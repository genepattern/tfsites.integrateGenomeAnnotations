# tfsites.IntegrateGenomeAnnotations v1

**Author(s):** Joe Solvason  

**Contact:** Joe Solvason (solvason@eng.ucsd.edu)

**Adapted as a GenePattern Module by:** Ted Liefeld (jliefeld@cloud.ucsd.edu)

**Task Type:** Transciption factor analysis

**LSID:**  urn:lsid:genepattern.org:module.analysis:00446


## Introduction

`IntegrateGenomeAnnotations` checks whether overlap exists between a list of mutations in a genotypic dataset and BED files containing genomic regions of interest. For each mutation, it is reported whether or not the region of each mutation overlaps with the regions contained within each BED file. 

## Methodology

The input file containing a list of mutations is converted from TSV to BED format, so that each mutation is denoted as a genomic interval. The tool `bedtools intersect` is used to search for overlap between the genomic intervals in the converted BED file and the intervals in each input BED file provided. For each input BED file, there is one column appended to the original genotypic dataset that indicates whether overlap exists. This column contains a 1 if there is overlap and 0 if there is no overlap. 

## Parameters

<span style="color: red;">*</span> indicates required parameter

### Inputs and Outputs 

- <span style="color: red;">*</span>**genotypic data (.tsv)**
    - File containing a list of mutations from a genotypic experiment, along with their genomic position. It can also contain columns with other information, such as the statistical association between the mutation and a phenotype. 
- <span style="color: red;">*</span>**BED genomic interval data (.bed)**
    -  One or more BED files containing a list of genomic intervals of interest. 
- <span style="color: red;">*</span>**genotypic and BED overlap (.tsv)**
    - Name of the output file containing the original genotypic file, along with additional columns that indicate whether overlap exists between each mutation and the genomic intervals from the genotypic data file(s). For each input BED file, there is one column appended to the original genotypic data file that indicates whether or not overlap exists.
 
### Other Parameters

- <span style="color: red;">*</span>**zero index genomic coordinates (boolean)**
    - If `True`, the genomic coordinates in the input genotypic file are 0-indexed (sequence numbering starts at 0). If `False`, they are 1-indexed (sequence numbering starts at 1).


## Input Files

1. genotypic data (.tsv)
- Can optionally contain other columns, but the first three columns (`Chromosome`, `Position`, `Ref`) below must be provided first
- Columns:
    - `Chromosome:` name of the chromosome
    - `Position:` genomic position of the mutation
    - `Ref:` reference nucleotide
    - `Alt:` alternate nucleotide
    - `P-value:` statistical association between the mutation and a phenotype

```
Chromosome   Position     Ref     Alt     P-value
chr1         1255143      C       T       1.43e-08
chr1         1258207      T       A       1.24e-09
chr1         1259091      C       A       1.75e-08
chr1         1259093      T       A       1.05e-08
chr1         1259424      T       C       3.17e-09
```
    
2. BED genomic interval data (.bed)
- Can provide more than one file
- Columns:
    - `Chromosome:` name of the chromosome
    - `Start:` start coordinate of genomic interval
    - `End:` end coordinate of genomic interval

file1
```
Chromosome   Start       End   
chr1	     1255130	 1255150
chr1	     1259080	 1259099
chr1	     1259410	 1259420
chr1	     1281630	 1281645
chr1	     1351740	 1351750
```

file2
```
Chromosome   Start       End  
chr1         1255135	 1255145
chr1         1259420	 1259428
chr1         1281200	 1281220
chr1         1325350	 1325365
chr1         1351740	 1351750
```

       
## Output Files

1. genotypic & BED overlap (.tsv)
- Can have more or less columns depending on the number of BED files provided
- Columns
    - `Chromosome:` name of the chromosome
    - `Position:` genomic position of the mutation
    - `Ref:` reference nucleotide
    - `Alt:` alternate nucleotide
    - `P-value:` statistical association between genotype and phenotype
    - `Overlap-{name of BED file #1}:` whether overlap exists between the genotypic data and BED file #1 
    - `Overlap-{name of BED file #2}:` whether overlap exists between the genotypic data and BED file #2
  
```
Chromosome   Position     Ref    Alt    P-value        Overlap-file1.bed    Overlap-file2.bed	
chr1	     1255143	  C      T      1.436e-08      1                    1
chr1         1258207      T      A      1.24e-09       0                    0
chr1         1259091      C      A      1.75e-08       0                    0
chr1	     1259093	  T      A      1.056e-08      1                    0
chr1	     1259424	  T      C      3.171e-09      0                    1
```
    
  
## Example Data

[Example input data is available on github](https://github.com/genepattern/tfsites.integrateGenomeAnnotations/gpunit/data)

    
## Version Comments

- **1.0.2** (2024-05-10): Draft updated for new parameter names and descriptions.
- **1.0.1** (2024-02-02): Draft completed.
- **1.0.0** (2023-11-27): Initial draft of document scaffold.
