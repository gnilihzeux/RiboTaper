# RiboTaper
**A copy RiboTaper v1.3.1a and some debugs by myself.**

The original RiboTaper is in [here](https://ohlerlab.mdc-berlin.de/software/RiboTaper_126/).


## Notice

### P-site definition

RiboTaper takes only 10% reads for P-site definition. But it is poor for the case with low seq depth.

**So, I adjust to 100% to adapt to all kinds of situations.**

### best & unique BAM

We could see from source script `Ribotaper.sh`

```
samtools view -b -q 50 $ribo_bam > RIBO_unique.bam 
samtools view -b -F 0X100 $ribo_bam > RIBO_best.bam 
```

It is ok for **STAR** aligner.

### bug fixed

1.`quality_check.R` line 114 & 118
