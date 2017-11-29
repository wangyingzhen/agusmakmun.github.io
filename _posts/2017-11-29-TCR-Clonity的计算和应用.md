---
layout: post  
title:  "TCR-多样性度量指标-Clonity的计算"  
date:   2017-11-29 00:00:00 +0700  

---

`TCR` `Clonity`   
### 几个相关概念  
**Diversity**: accounts for both “richness” and “evenness” components ( Shannon’s entropy).  
**Richness**：The number of different specificities in the sample (counting the number of unique antigen receptor sequences).  
**Eveness**：relative abundance of these different specificities ( gini index, clonality, 1- Pielou’s evenness).  
**Clonality**：values range from 0 to 1 and describe the shape of the frequency distribution: clonality values approaching 0 indicate a very even distribution of frequencies, whereas values approaching 1 indicate an increasingly asymmetric distribution in which a few clones are present at high frequencies.

### 计算公式
1.先计算信息熵  
![](https://note.youdao.com/yws/api/personal/file/9155277764A040078183A37CF3AA4F3C?method=download&shareKey=d0199ed4f0f3259677d1089cfd2d22ea)   
2. normalized and inverted(This conversion is intended to generate values that agree with intuition)  
![](https://note.youdao.com/yws/api/personal/file/973BDE1777A94D188D9A53040B45C322?method=download&shareKey=61f72111681b7c8268ae2be8c5d1c49c)

### 相关应用
拒文献报道，Clonity与PD-1,CTLA-4抗体治疗的预后相关，另外和药物毒性也有关联。 
 
[1]Tumeh P C, Harview C L, Yearley J H, et al. PD-1 blockade induces responses by inhibiting adaptive immune resistance[J]. Nature, 2014, 515(7528):568.  
[2] Robert L, Tsoi J, Wang X, et al. CTLA4 blockade broadens the peripheral T-cell receptor repertoire[J]. Clinical Cancer Research An Official Journal of the American Association for Cancer Research, 2014, 20(9):2424.  
[3]Cooper Z A, Frederick D T, Juneja V R, et al. BRAF inhibition is associated with increased clonality in tumor-infiltrating lymphocytes[J]. Oncoimmunology, 2013, 2(10):-.  
[4]Lavin Y, Kobayashi S, Leader A, et al. Innate Immune Landscape in Early Lung Adenocarcinoma by Paired Single-Cell Analyses[J]. Cell, 2017, 169(4):750.  
[5]Kirsch I, Vignali M, Robins H. T-cell receptor profiling in cancer ☆[J]. Molecular Oncology, 2015, 9(10):2063-2070.




-------------
*Author*: 王英珍   
*qq*: 296085360  
*email*:wangyingzhen91@163.com  