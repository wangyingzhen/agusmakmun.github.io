---
layout: post  
title:  "Rosalind-Counting-Point-Mutations"  
date:   2017-07-11 17:54:23 +0700  

---

`Rosalind` `perl`

### [Counting-Point-Mutations](http://rosalind.info/problems/grph/)   
### perl script:

	#!/usr/bin/perl -w
	use strict;
	use warnings;
	open(IN,"<",$ARGV[0]) or die $!;
	my %hash1;
	my %hash2;
	my @head;
	$/=">";
	while (<IN>){
	chomp;
	next if (/^$/);
	my ($head,$seq)=split /\n/,$_;
	$seq=~s/\n//g;
	my $start=substr($seq,0,3);
	my $end=substr($seq,-3,3);
	$hash1{$head}=$start;
	$hash2{$head}=$end;
	push @head,$head;
	}
	my %hash3;
	for my $head(@head){
	for my $head1(@head){
	next if ($head eq $head1);
	if ($hash2{$head} eq $hash1{$head1}){
	$hash3{$head}{$head1}=0;
	}
	if ($hash2{$head1} eq $hash1{$head}){
	$hash3{$head1}{$head}=0;
	}
	}
	}
	for my $key(keys %hash3){
	for my $key1(keys %{$hash3{$key}}){
	print $key,"\t",$key1,"\n";
	}
	}


               

-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyingzhen91@163.com  
