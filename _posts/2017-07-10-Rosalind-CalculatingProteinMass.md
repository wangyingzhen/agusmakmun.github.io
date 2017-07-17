---
layout: post  
title:  "Rosalind-REVP-Locating_Restriction_Sites"  
date:   2017-07-08 17:54:23 +0700  

---
`Rosalind` `perl`

### [PRTM]：[Calculating Protein Mass](http://rosalind.info/problems/prtm/)

#### perl script
    
    #!/usr/bin/perl -w  
    use strict;
    my %hash=(A=>"71.03711",C=>"130.0919",D=>"115.02694",E=>"129.04259",F=>"147.06841",G=>"57.02146",H=>"137.05891",I=>"113.08406",K=>128.09496,L=>"113.08406",M=>"131.04049",
    N=>"114.04293",P=>"97.05276",Q=>"128.05858",R=>"156.10111",S=>"87.03203",T=>"101.04768",V=>"99.06841",W=>"186.07931",Y=>"163.06333");
    open (IN,"<$ARGV[0]");  
    my $seq=<IN>;  
    chomp $seq;
    my @arr=split //,$seq;
    my $tol=0;
    foreach my $arr(@arr){$tol+=$hash{$arr}};
    print $tol;


markdown 不知道怎么换行真是头疼。。。后边再改进吧

-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyz666@outlook.com  
