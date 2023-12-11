# tfsites.IntegrateGenomeAnnotations v1

**Author(s):** Joe Solvason  

**Contact:** Joe Solvason (solvason@eng.ucsd.edu)

**Adapted as a GenePattern Module by:** Ted Liefeld (jliefeld@cloud.ucsd.edu)

**Task Type:** Transciption factor analysis

**LSID:**  urn:lsid:genepattern.org:module.analysis:00446


## Introduction

tfsites.IntegrateGenomeAnnotations finds all possible SNVs and their effects on binding sites.

## Functionality

TBD

## Methodology

TBD

## Parameters

<span style="color: red;">*</span> indicates required parameter

- **input data**<span style="color: red;">*</span>
    - This is a [ state what the format and content is supposed to be] list of SNVs to be analyzed.
- **zero.position**<span style="color: red;">*</span>
    -  TRUE/FALSE, genomic coordinates are 0-indexed 
- **out filename**<span style="color: red;">*</span>
    - Out file name for the annotated PBM data
- **bed file**
    - [Optional] Bed file to overlap with genomic coordinates in input file.


## Input Files

1. input data.  Tab delimited file [ define format and contents in detail ] 
    
2. bed file. Bed file to overlap with genomic coordinates in input file. 

       
## Output Files

  1.TSV: <input.data_basename>.bed-overlap.tsv.  Tab-separated text file TBD.
    e.g. 
```
chrom	pos-1idx	ref	alt	info    <first bed file name> <second bed file name>	
chr1	1255143	C	T	1.436e-08	1	1
chr1	1259093	T	A	1.056e-08	1	0
chr1	1259424	T	C	3.171e-09	0	1

```
    
  
## Example Data

[Example input data is available on github](https://github.com/genepattern/tfsites.integrateGenomeAnnotations/gpunit/data)
    
## References

    
## Version Comments

- **1.0.0** (2023-11-27): Initial draft of document scaffold.
