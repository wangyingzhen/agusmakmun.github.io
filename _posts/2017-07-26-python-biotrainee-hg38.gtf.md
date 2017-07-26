---
layout: post  
title:  "python-biotrainee-test3-hg38.gtf"  
date:   2017-07-26 14:26:13 +0700  

---
`python` `hg38.gtf`

### test
对hg38的gtf文件进行探究（每条染色体基因数目统计等等）

### data
    wget ftp://ftp.ensembl.org/pub/release-87/gtf/homo_sapiens/Homo_sapiens.GRCh38.87.chr.gtf.gz

### python
    	#!/usr/bin/python
	import time
	import sys
	from collections import OrderedDict
	dic= OrderedDict()
	list_chr=[]
	list_type=['gene','transcript','exon','CDS']
	start=time.clock()
	with open(sys.argv[1],"r") as f:
		for line in f:
			if line.startswith('#'):
				continue
			line=line.rstrip()
			chr=line.split('\t')[0]
			gene_type=line.split('\t')[2]
			if not chr in list_chr:
				list_chr.append(chr)
				dic[chr]={} ##此处应该是建造一个二维的字典
				for type1 in list_type:
					dic[chr][type1]=0
			if gene_type in list_type:
				dic[chr][gene_type]+=1
	sorted(dic.keys())
	for head,seq in dic.items():
		print head,
		for i in list_type:
			print i,dic[head][i],
		print "\n",

### result
    1 gene 5194 transcript 17296 exon 108417 CDS 64975
	2 gene 3971 transcript 14390 exon 91110 CDS 53480
	3 gene 3010 transcript 12064 exon 74562 CDS 43036
	4 gene 2505 transcript 7732 exon 45520 CDS 27178
	5 gene 2868 transcript 9200 exon 52715 CDS 30758
	6 gene 2863 transcript 8540 exon 52060 CDS 33020
	7 gene 2867 transcript 9437 exon 56882 CDS 32904
	X gene 2359 transcript 6037 exon 35309 CDS 22767
	8 gene 2353 transcript 7717 exon 42730 CDS 24440
	9 gene 2242 transcript 6581 exon 42213 CDS 26270
	11 gene 3235 transcript 12151 exon 69915 CDS 42363
	10 gene 2204 transcript 6507 exon 41978 CDS 26710
	12 gene 2940 transcript 11419 exon 69686 CDS 42166
	13 gene 1304 transcript 3236 exon 18266 CDS 10435
	14 gene 2224 transcript 7476 exon 41897 CDS 24528
	15 gene 2152 transcript 7444 exon 45517 CDS 26068
	16 gene 2511 transcript 9896 exon 57261 CDS 32673
	17 gene 2995 transcript 12573 exon 74785 CDS 44869
	18 gene 1170 transcript 3640 exon 20309 CDS 11850
	20 gene 1386 transcript 4242 exon 25502 CDS 15499
	19 gene 2926 transcript 12695 exon 71424 CDS 43907
	Y gene 523 transcript 740 exon 3784 CDS 1538
	22 gene 1318 transcript 4472 exon 26063 CDS 14888
	21 gene 835 transcript 2413 exon 13966 CDS 7396
	MT gene 37 transcript 37 exon 37 CDS 13


### shell
    cat Homo_sapiens.GRCh38.87.chr.gtf |awk '$3~/gene/{print $1,$3}'|sort|uniq -c|less -S
  
### perl one line
    cat Homo_sapiens.GRCh38.87.chr.gtf.gz|perl -lane 'next if /^#/;if $F[2] eq 'gene'{print}'|sort|uniq -c|less -S

---------
*放慢脚步,深耕细作。*