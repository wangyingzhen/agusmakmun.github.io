---
layout: post  
title:  "TCR pipeline"  
date:   2017-10-09 00:00:00 +0700  

---

`TCR` `MIXCR` `pipeline`    
 
	###mixcr####
	for i in `seq 42 50`
	do
	sample=R71090$i;
	read1=R71090$i*R1*;
	read2=R71090$i*R2*;
	echo `date` "start do mixcr for " $sample;
	mixcr align -r $sample"_log.txt" $read1 $read2 $sample"_alignments.vdjca"
	mixcr assemble -r $sample"_log.txt" $sample"_alignments.vdjca" $sample"_clones.clns"
	mixcr exportClones -o -t -c TRB --preset-file myFields.txt $sample"_clones.clns" $sample"_TRB.clones.txt"
	mixcr exportClones -o -t -c TRA --preset-file myFields.txt $sample"_clones.clns" $sample"_TRA.clones.txt"
	echo `date` "end do mixcr for " $sample;
	done  
	###qc_log###  
	 for i in *log.txt; 
	 do 
	 echo $i;
	 grep "Total sequencing reads" $i;
	 grep "Successfully aligned reads" $i;
	 grep "Reads used in clonotypes, percent of total" $i;
	 grep "Final clonotype count" $i;
	 done

	
	######add1. myFields.txt####
	-cloneId
	-count
	-fraction
	-vHit
	-dHit
	-jHit
	-aaFeature CDR3
	######add2. log.txt####
	Total sequencing reads
	Successfully aligned reads
	Alignment failed, no hits
	Alignment failed because of absence of V hits
	Alignment failed because of absence of J hits
	Alignment failed because of low total score
	Reads used in clonotypes, percent of total
	Reads dropped due to the lack of a clone sequence: 82394 (8.12%)
	Reads dropped due to failed mapping
	Reads dropped with low quality clones
	Final clonotype count
	TRB chains






-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyingzhen91@163.com   
