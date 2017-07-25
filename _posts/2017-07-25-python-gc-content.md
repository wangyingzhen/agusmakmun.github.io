---
layout: post  
title:  "python-GC-content"  
date:   2017-07-25 15:56:13 +0700  

---
`python` `GCcontent`



### data
	>chr_1
	atcgaatt
	>chr_2
	atcgc
	gat
	>chr_3
	atcgCGcgat
	>chr_4
	CGCGCGcgcg

### python
	#!/usr/bin/python
	import sys
	def gc(seq):
		seq=seq.upper()
		return (float(seq.count("G")+seq.count("C"))/len(seq))

	f=open(sys.argv[1],"r")

	dic={}
	for line in f:
		line=line.strip()
		if line.startswith('>'):
			head=line
			dic[head]=""
		else:
			dic[head]+=line
	for head,seq in dic.items(): ##
		print head
		print gc(seq)

