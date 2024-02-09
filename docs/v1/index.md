# tfsites.IntegrateGenomeAnnotations v1

**Author(s):** Joe Solvason  

**Contact:** Joe Solvason (solvason@eng.ucsd.edu)

**Adapted as a GenePattern Module by:** Ted Liefeld (jliefeld@cloud.ucsd.edu)

**Task Type:** Transciption factor analysis

**LSID:**  urn:lsid:genepattern.org:module.analysis:00446


## Introduction

`integrateGenomeAnnotations` checks whether overlap exists between a list of mutations in a genotypic dataset and BED files containing genomic regions of interest. For each mutation, it is reported whether or not the region of each mutation overlaps with the regions contained within each BED file. 

## Methodology

The input file containing a list of mutations is converted from TSV to BED format, so that each mutation is denoted as a genomic interval. Bedtools intersect is used to search for overlap between the genomic intervals in the converted BED file and the intervals in each input BED file provided. For each input BED file, there is one column appended to the original genotypic dataset that indicates whether overlap exists (1 if there is overlap and 0 if there is not). 

## Parameters

<span style="color: red;">*</span> indicates required parameter

### Inputs and Outputs 

- <span style="color: red;">*</span>**Genotypic Data Input (.tsv)**
    - This file contains a list of mutations from a genotypic experiment, along with their genomic position. It can also contain columns with other information, such as the statistical association between the mutation and a phenotype. 
- <span style="color: red;">*</span>**BED Genomic Interval Data (.bed)**
    -  This file contains a list of genomic intervals of interest. 
- <span style="color: red;">*</span>**Genotypic and BED Overlap (.tsv)**
    - Out file name for the annotated PBM data
 
### Other Parameters

- **Zero Index Genomic Coordinates (boolean)**
    - If `True`, the genomic coordinates in the input eQTL file are 0-indexed (sequence numbering starts at 0). If `False`, they are 1-indexed (sequence numbering starts at 1).


## Input Files

1. Genotypic Data Input (.tsv)
- Can optionally contain other columns, but the five columns below must be listed first
- Columns:
    - `Chrom:` name of the chromosome
    - `Pos:` genomic coordinate indicating the position of the mutation
    - `Ref:` the wildtype sequence 
    - `Alt:` the mutated sequence
    - `P_value:` statistical association between the mutation and a phenotype

```
chrom    pos      ref  alt  p_value
chr1     1255143  C    T    1.43e-08
chr1     1259093  T    A    1.05e-08
chr1     1259424  T    C    3.17e-09
```
    
2. BED Genomic Interval Data (.bed)
- Can provide more than one file 
- Columns:
    - `Chrom:` name of the chromosome
    - `Start:` starting position of the genomic interval
    - `End:` ending position of the genomic interval

```
chrom   start    end   
chr1	1255130	 1255150
chr1	1259080	 1259099
chr1	1259410	 1259420
chr1	1281630	 1281645
chr1	1351740	 1351750
```

```
chrom   start    end  
chr1	1255135	 1255145
chr1	1259420	 1259428
chr1	1281200	 1281220
chr1	1325350	 1325365
chr1	1351740	 1351750
```

       
## Output Files

  1.Genotypic and BED Overlap (.tsv)
- Columns:
    - `Chrom:` name of the chromosome
    - `Pos:` genomic coordinate indicating the position of the mutation
    - `Ref:` the wildtype sequence
    - `Alt:` the mutated sequence
    - `P_value:` statistical association between the mutation and a phenotype
    - `Overlap-[BED Genomic Interval Data #1]:` whether overlap exists between the mutations from the genotypic dataset and any genomic intervals contained in BED Genomic Interval Data #1 (1 if there is an overlap, 0 if there is no overlap)
    - `Overlap-[BED Genomic Interval Data #2]:` whether overlap exists between the mutations from the genotypic dataset and any genomic intervals contained in BED Genomic Interval Data #2 (1 if there is an overlap, 0 if there is no overlap)
  
```
chrom	pos-1idx	ref	 alt	info          overlap-file1.bed    overlap-file2.bed	
chr1	1255143	        C	 T      1.436e-08     1                    1
chr1	1259093	        T	 A      1.056e-08     1                    0
chr1	1259424	        T	 C      3.171e-09     0                    1
```
    
  
## Example Data

[Example input data is available on github](https://github.com/genepattern/tfsites.integrateGenomeAnnotations/gpunit/data)

    
## Version Comments

- **1.0.0** (2023-11-27): Initial draft of document scaffold.
- **1.0.1** (2024-02-02): Draft completed.
