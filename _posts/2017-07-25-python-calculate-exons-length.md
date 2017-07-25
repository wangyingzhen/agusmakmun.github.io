---
layout: post  
title:  "python-calculate-exons-length"  
date:   2017-07-25 14:57:13 +0700  

---
`python` `exonlength`

## python-calculate-exons-length

	#!/usr/bin/python
	import sys
	import re
	f=open(sys.argv[1],"r")  #传参
	sum=0
	list=[]
	for line in f:
	        if line.startswith('#'): #判断开头
	                continue         #跳过    
	        line=line.rstrip()       #相当于perl的chomp    
	        exons=re.findall('[0-9]+-[0-9]+',line) #正则，返回列表
        	for exon in exons:
            	    list.append(exon)
	st=set(list)                    #去重
	for i in st:                    
    	    exon_one=i.split('-')   
    	    exon_start=exon_one[0]
    	    exon_end=exon_one[1]
    	    sum+=int(exon_end)-int(exon_start)
	print sum
```

## data
	wget ftp://ftp.ncbi.nlm.nih.gov/pub/CCDS/current_human/CCDS.20160908.txt