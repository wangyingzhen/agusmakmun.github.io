---
layout: post  
title:  "Finding-a-Shared-Motif"  
date:   2017-07-05 12:11:13 +0700  

---

`perl` `Rosalind`

## [LCSM]:[Finding a Shared Motif](http://rosalind.info/problems/lcsm/)
###perl script

	#!/usr/bin/perl -w  
	use strict;  
	use warnings;
	use Getopt::Long;
	use Data::Dumper;
	use FindBin qw($Bin $Script);
	use File::Basename qw(basename dirname);
	my $BEGIN_TIME=time();
	my $version="1.0.0";
	#######################################################################################

	# ------------------------------------------------------------------
	# GetOptions
	# ------------------------------------------------------------------
	my ($infile,$outfile);
	GetOptions(
                                "help|?" =>\&USAGE,
                                "i:s"=>\$infile,
                                "o:s"=>\$outfile,
                                ) or &USAGE;
	&USAGE unless ($infile );
	#######################################################################################
	# ------------------------------------------------------------------
	# Main Body
	# ------------------------------------------------------------------
	open (IN,"<",$infile) or die $!;
	open (OUT,">",$outfile) or die $!;
	$/=">";
	my %head_seq;
	my @motif;
	my %len_motif;
	my $k=0;
	while (<IN>) {
        	chomp;
	next if (/^$/);
        $k++;
        my ($head,$seq)=split /\n/,$_,2;
        $seq=~s/\n//g;
        $head_seq{$head}=$seq;
        my @arr=split//,$seq;
        if ($k==1) {
                for (my $i=2;$i<@arr;$i++) {
                        for (my $j=0;$j<@arr;$j++) {
                                my $motif=substr("$seq",$j,$i);
                                push @motif,$motif;
                        }
                }
        }
        else{
                next;
        }
	}
	for my $motif (@motif) {
        $a=0;
        for my $key(keys %head_seq){
                if ($head_seq{$key}=~/$motif/) {
                        $a++;
                }
                else{
                        next;
                }
                if ($a==$k) {
                        $len_motif{length($motif)}{$motif}=1;
                }
        }
	}
	for my $key(sort {$b<=>$a} keys %len_motif) {
        for my $key1(keys %{$len_motif{$key}}) {
                print OUT $key,"\t",$key1,"\n";die;
        }
	}
	#######################################################################################
	print STDOUT "\nDone. Total elapsed time : ",time()-$BEGIN_TIME,"s\n";
	#######################################################################################

	# ------------------------------------------------------------------


	sub GetTime {
        my ($sec, $min, $hour, $day, $mon, $year, $wday, $yday, $isdst)=localtime(time());
        return sprintf("%4d-%02d-%02d %02d:%02d:%02d", $year+1900, $mon+1, $day, $hour, $min, $sec);
	}


	sub USAGE {#
        my $usage=<<"USAGE";
	Program:
	Version: $version
	Contact: Wang_yingzhen<xiangshu007\@qq.com>
	Description:

	Usage:
	 Options:
        -i      <infile>        input file,
        -o      <outfile>       output file,
        -h                              Help

	USAGE
        print $usage;
        exit;
	}


