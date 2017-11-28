---
layout: post  
title:  "TCR pipeline V1.0"  
date:   2017-11-03 00:00:00 +0700  

---

`TCR` `MIXCR` `pipeline`    
## 1. 主程序 tcr.pl ##

    #!/usr/bin/perl -w
    use strict;
    use warnings;
    use Getopt::Long;
    use Data::Dumper;
    use lib qw(/home/yzwang/soft/perl/lib_myself/YAML-Tiny-1.70/lib);
    use YAML::Tiny ;
    #use Pipeliner ;
    use FindBin qw($Bin $Script);
    use File::Basename qw(basename dirname);
    my $BEGIN_TIME=time();
    my $version="1.0.0";
    #######################################################################################
    
    ## ------------------------------------------------------------------
    # GetOptions
    # # ------------------------------------------------------------------
    my ($infile,$outfile);
    GetOptions(
    "help|?" =>\&USAGE,
    "i:s"=>\$infile,
    "o:s"=>\$outfile,
    ) or &USAGE;
    &USAGE unless ($infile );
    my $yamlfile=$infile;
    my $main=YAML::Tiny::LoadFile($yamlfile);
    my @samples=keys %{$main->{"Project"}{"Samples"}};
    my $sample_type= $main->{"Project"}{"sample_type"};
    my $cmd ="";
    print STDERR "\n\n\n--------------------------------------------------------------------------------\n"
      ."---------------------run mixcr get the CDR3 information   --------------------------------------\n"
      ."--------------------------------------------------------------------------------\n\n\n";
    for (my $i=0;$i<@samples;$i++) {
    mkdir $samples[$i] unless (-d $samples[$i]);
    my $cmd= "mixcr align -r $samples[$i]/$samples[$i].log.txt $main->{Project}{Samples}{$samples[$i]}{read1} $main->{Project}{Samples}{$samples[$i]}{read2} $samples[$i]/$samples[$i].alignments.vdjca";
    unless (-e "$samples[$i]/$samples[$i].alignments.vdjca") {
    &process_cmd($cmd);
    }
    
    my $cmd1= "mixcr assemble -r $samples[$i]/$samples[$i].log.txt $samples[$i]/$samples[$i].alignments.vdjca $samples[$i]/$samples[$i].clones.clns";
    unless (-e "$samples[$i]/$samples[$i].clones.clns") {
    &process_cmd($cmd1);
    }
    my $cmd2= "mixcr exportClones  -o -t -c $main->{Project}{sample_type} --preset-file $main->{Project}{output_type} $samples[$i]/$samples[$i].clones.clns $samples[$i]/$samples[$i].TRB.clones.txt";
    unless (-e "$samples[$i]/$samples[$i].TRB.clones.txt") {
    &process_cmd($cmd2);
    }
    
    my $cmd3= "perl  $main->{Project}{tj} $samples[$i]/$samples[$i].TRB.clones.txt $samples[$i]/$samples[$i].TRB.clones.txt >$samples[$i]/$samples[$i].TRB.clones.tj";
    unless (-e "$samples[$i]/$samples[$i].TRB.clones.tj") {
    &process_cmd($cmd3);
       }
    `grep "Total sequencing reads"  $samples[$i]/$samples[$i].log.txt >$samples[$i]/qc.txt`;
    `grep "Successfully aligned reads"  $samples[$i]/$samples[$i].log.txt >>$samples[$i]/qc.txt`;
    `grep "used in clonotypes, percent of total"  $samples[$i]/$samples[$i].log.txt >>$samples[$i]/qc.txt`;
    `grep "Final clonotype count"  $samples[$i]/$samples[$i].log.txt >>$samples[$i]/qc.txt`;
    }
    #######################################################################################
    print STDOUT "\nDone. Total elapsed time : ",time()-$BEGIN_TIME,"s\n";
    ########################################################################################
    # ------------------------------------------------------------------
    sub process_cmd {
    my ($cmd) = @_;
    
    print STDERR &GetTime."CMD: $cmd\n" ;
    
    my $start_time = time();
    my $ret = system("bash", "-c", $cmd);
    my $end_time = time();
    
    if ($ret) {
    
    die "Error, cmd: $cmd died with ret $ret";
    }
    
    print STDERR "CMD finished (" . ($end_time - $start_time) . " seconds)\n" ;
    
    return;
    }
    sub GetTime {
    my ($sec, $min, $hour, $day, $mon, $year, $wday, $yday, $isdst)=localtime(time());
    return sprintf("%4d-%02d-%02d %02d:%02d:%02d", $year+1900, $mon+1, $day, $hour, $min, $sec);
    }
    
    
    sub USAGE {#
    my $usage=<<"USAGE";
    Program:
    Version: $version
    Contact: yzwang <wangyingzhen91\@163.com> <296085360\@qq.com>
    Description:
    
    Usage:
      Options:
    -i  <infile>YAML config file
    -h  Help
    
    USAGE
    print $usage;
    exit;
    }
    


## 2. 配置文件 tcr.yaml##
    Project:
    	Samples:
    	T01:
   			read1 : /home/yzwang/project/001_170922_MN00561_0029_A000H23KFF/data/cleandata/R7109039/R7109039_PLSC_WBC_L001.R1.clean.fq.gz
    		read2 : /home/yzwang/project/001_170922_MN00561_0029_A000H23KFF/data/cleandata/R7109039/R7109039_PLSC_WBC_L001.R2.clean.fq.gz
    	T02:
    		read1 : T03_read1_R1_001.fastq.gz#MJ-gen
    		read2 : T03_read2_R2_001.fastq.gz
    
    	sample_type : TRB   # TRB or TRA or IGH or IGL or IGK
    	output_type : /projects/TCR_pool/03.171028_K00259_0038_AHKYJWBBXX/02.script/myFields.txt
    	mixcr       : ~/soft/mixcr/mixcr-2.1.5_new/mixcr
    	tj          : ~/project/002_170929_MN00561_0032_A000H23VTG/rawdata/tmp.pl


## 3. 运行方法： ##
	首先填写配置文件，填入fq数据文件和样品类型（TRB or others）；
	然后执行程序：nohup perl tcr.pl tcr.yaml &
	


-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyingzhen91@163.com   
