## Codes for calculating N-index in cfDNA data for Ju et al.

The main program is `calc.N-index`, you can run it without parameters to see the usage:
```
Usage: /mnt/github/N-index/calc.N-index <genome.info> <nucleosome.center.bed[.gz]> <mask.bed> <PE.bed.list>

Written by Kun Sun (sunkun@szbl.ac.cn). (c) Shenzhen Bay Laboratory.

This program is designed to calculate N-index for each sample in 'bed.list',
which should contain (at least) 2 columns: sampleID and /path/to/bed[.gz].
The current program only supports Paired-End data; gzipped bed file is supported.
For 'mask.bed', you can set to '/dev/null' if you do not want to use it.

Output: Sid Total #IND #ANY #Both %IND/2 %ANY %Both

Counting mode explaination:
	IND : count U and D ends independently (feature for cancer diagnosis)
	ANY : count the fragment if U OR  D end falls in nucleosome core
	BOTH: count the fragment if U AND D ends fall in nucleosome core

```
There are 4 compulsory paramters:
1. `genome.info` contains the size information for each chromosome in human genome,
and we had provided a `hg38.info` file in this package;
2. `nucleosome.center.bed` contains the center loci annotations, and we used
[this file downloaded from NucMap](https://download.cncb.ac.cn/nucmap/organisms/v1/Homo_sapiens/byDataType/Nucleosome_peaks_DANPOS/Homo_sapiens.hsNuc0390101.nucleosome.DANPOSPeak.bed.gz), which is the same to the one used in
[An et al. Nature Communications 2023](https://www.nature.com/articles/s41467-023-35959-6);
3. `mask.bed` contains problematic regions, and we had provided a
`ENCODE.blacklist.hg38.bed` file in this package (collected from
[Amemiya et al. Scientific Reports 2019, 9:9354](https://www.nature.com/articles/s41598-019-45839-z));
4. `PE.bed.list` file contains sample IDs and path to the bed files in 2-column format, and the users
should prepare this file themselves.

For outputs, we used the `%IND/2` (the 6th column) as the N-index for each sample.

