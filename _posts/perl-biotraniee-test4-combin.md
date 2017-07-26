---
layout: post  
title:  "perl-shell-biotrainee-test4-combin"  
date:   2017-07-08 17:54:23 +0700  

---

`perl` `combin` `shell`


### data
    cat >tmp.sh
    perl '{print "gene_$_\t".int(rand(1000))foreach 1..100}'
    for i in `seq 10`
    do
    sh tmp.sh >num_$i.txt
    done
### perl
    #!usr/bin/perl -w
    use strict;
    my @file=glob"*.txt";
    my %hash;
    for my $file (@file){
            open(FH,"<",$file);
            while(<FH>){
                    chomp;
                    my @arr=split /\t/,$_;
                    $hash{$arr[0]}{$file}=$arr[1];
            }
    }
    for my $key (keys %hash){
            print $key;
            for my $file (@file){
                    print "\t",$hash{$key}{$file};
            }
            print "\n";
    }
### shell+R
    >shell
    awk 'print FLIENAME"\t"$0' *.txt >tmp.txt
    >R
    data=read.table('tmp.txt',sep = '\t',stringsAsFactors = F)
    library(reshape2)
    fpkm <- dcast(data,formula = V2~V1)

参考 [biotrainee.com](http://www.biotrainee.com/thread-603-1-1.html)

----------------------
*磨刀不误砍柴工*