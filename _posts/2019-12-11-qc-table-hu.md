---
layout: post
title: "qc-hu"
date: 2019-12-11
tag: sas
---





qctable-hu

```sas
***********************Program info**********************************
* Copyright (c)    	        : The pgm codes belong to Knowlands property.
* Project Code/Sponsor Name	: SSGJ-602-mCRC-I-02-IDMC/三生国健药业（上海）股份有限公司;
* Program Name     	        : SSGJ-602-mCRC-I-02-IDMC_TFL_v10_qc.sas
* Purpose          	        : 比对TFL
* Programmer/Date 	        : Hu Cao/Nov 8, 2019
* Input dataset(s)          : E:\SSGJ-602-mCRC-I-02-IDMC\3 STATISTICS\Data Monitoring Committee\DMC_TFL\TFL_v1.0\ads.adsl、adae、adlb、adeg、advs、adpe、adcm、adex、admh、adpc、adpp、adpp_dummy、adpr、adsu、adsv
* Output			 	    : &study\3 STATISTICS\Table Figure Listing\
* External macros used      : 
* SAS Version               : 9.4
********************************************************************;


libname ads 'E:\SSGJ-602-mCRC-I-02-IDMC\3 STATISTICS\Data Monitoring Committee\DMC_data\ADS_v1.0';



/*表14.1.1 受试者分布*/
proc sql;
create table treat_random as
select '随机' as label ,ARM as actarm,count(distinct usubjid) as peop_count from ads.adsl
where RANDFL='Y' group by ARM;quit;
%macro treat1(name=,condition=,condition_aval=);
proc sql;
create table treat_&condition as
select &name as label,ACTARM,count(distinct usubjid) as peop_count from ads.adsl 
where &condition=&condition_aval
group by actarm;
quit;
%mend;
%treat1(name='complete',condition=EOSSTT,condition_aval='是');
%macro treat2(name=,condition=);
proc sql;
create table treat_&condition as
select &name as label,ACTARM,count(distinct usubjid) as peop_count from ads.adsl 
where &condition is not missing
group by actarm;
quit;
%mend;
%treat2(name='get',condition=DOSEA);
%treat2(name='quit',condition=DCSREAS);
proc sql;
create table treat_uncomreason as
select '提前中止研究原因' as label,actARM,DCSREAS,count(distinct usubjid) as peop_count from ads.adsl
where DCSREAS is not missing  group by actARM,DCSREAs;quit;
data sum_treat;
set treat:;
run;

 
/*表14.1.2 分析人群*/
/*随机人群按计划分组，其他人群按实际分组*/
proc sql;
create table people_randfl as
select 'randfl' as label ,ARM as actarm,count(distinct usubjid) as peop_count from ads.adsl
where randfl='Y' group by ARM;
quit;
%macro people_random1(people=,people_=);
proc sql;
create table people_&people as
select &people_ as label ,actARM,count(distinct usubjid) as peop_count from ads.adsl
where &people='Y' group by actARM;
quit;
%mend;
%people_random1(people=saffl,people_='saffl');
%people_random1(people=PKCSFL,people_='PKCSFL');
%people_random1(people=PKPSFL,people_='PKPSFL');
data sum_people;
set people:;
run;


/*表14.1.3 受试者随机入组时间分布表*/
proc sql;
create table random as
select RANDMOTH,ARM,count(distinct usubjid) as peop_count from ads.adsl
where RANDSTTN=1
group by RANDMOTH,ARM
order by ARM desc,RANDMOTH;
quit;


/*表14.1.4 受试者访视情况总结表*/
proc sql;
create table visit as
select VISIT,ACTARM,count(distinct usubjid) as peop_count from ads.adsv
where SAFFL='Y' 
group by VISIT,ACTARM
order by ACTARM desc,VISIT;
quit;


/*表14.1.5 人口学特征*/
/*安全集*/
data adsl;
set ads.adsl;
if SAFFL='Y' then output;
run;
/*不分组*/
ods output means.summary=adsl_sum1;
proc means data=adsl n mean std max min median q1 q3;
var age HEIGHTBL WEIGHTBL BMIBL BSABL;
quit;
ods output close;
/*分组*/
ods output means.summary=adsl_sum2;
proc means data=adsl n mean std max min median q1 q3;
var age HEIGHTBL WEIGHTBL BMIBL BSABL;
class ACTARM;
quit;
ods output close;
/*姓名，民族*/
proc sql;
create table adsl_sum3 as
select ETHNIC,SEX,ACTARM,count(distinct usubjid) as peop_count from adsl
group by ETHNIC,SEX,ACTARM
order by ETHNIC,SEX,ACTARM desc;
quit;


/*表14.1.6.1 既往病史情况总结*/
proc sql;
create table ill_past as
select ACTARM,count(distinct usubjid) as peop_count,MHSOC,MHTERM from ads.admh
where SAFFL='Y' and MHCAT like '%既往病史'
group by ACTARM,MHSOC,MHTERM;
quit;


/*表14.1.6.2 合并用药情况总结*/;
proc sql;
create table med_comb1 as
select ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from ads.adcm
where CMCAT='合并用药'
group by ACTARM;
quit;
/*到atc*/
proc sql;
create table med_comb2 as
select ATC2,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from ads.adcm
where CMCAT='合并用药'
group by ATC2,ACTARM
order by ATC2,ACTARM desc;
quit;

/*分药*/
proc sql;
create table med_comb3 as
select ATC2,CMPTNAM,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from ads.adcm
where CMCAT='合并用药'
group by ATC2,CMPTNAM,ACTARM
order by ATC2,CMPTNAM,ACTARM desc;
quit;


/*表14.3.1.1 所有TEAE发生情况总结*/;
/*TEAE*/
data adae;
set ads.adae;
if SAFFL = 'Y' and TRTEMFL ='Y' then output;
run;
/*最差严重程度*/;
proc sql;
create table max_ae as
select usubjid,max(aesevn) as max_ae from adae
group by usubjid;
quit;
proc sql;
create table union_ae as
select a.*,b.max_ae from adae as a
left join max_ae as b
on a.usubjid = b.usubjid;
quit;

proc sql;
create table teae311_sum0 as
select "sum" as label,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
group by ACTARM;
quit;
/*分级*/
proc sql;
create table teae311_sum as
select "分级sum" as label,ACTARM,max_ae,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
where max_ae = AESEVN 
group by max_ae,ACTARM;
quit;

/*/*检查最差严重程度2级的受试者的一级teae*/*/
/*proc sql;*/
/*create table te_ae311_1_2 as */
/*select "分级sum" as label,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae*/
/*where max_ae > AESEVN and SAFFL = 'Y' and TRTEMFL ='Y'*/
/*group by max_ae,ACTARM;*/
/*quit;*/;

/*严重不良事件，药物不良事件等总结*/
%macro teae_sum(name=,condition=,condition_aval=);
proc sql;
create table teae311_&condition as
select &name as label,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae 
where &condition=&condition_aval 
group by actarm;
quit;
%mend;
%teae_sum(name='SAE',condition=AESER,condition_aval='是');
%teae_sum(name='ADR',condition=AEDRUG,condition_aval='Y');
proc sql;
create table teae311_sum3 as
select "严重药物不良反应" as label,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae 
where AEDRUG='Y' and AESER='是'
group by actarm;
quit;
%teae_sum(name='die',condition=AEout,condition_aval='死亡');
%teae_sum(name='quit',condition=AEDIS,condition_aval='是');

data sum_teae311;
set teae311:;
run;


/*表14.3.3.1 TEAE总结*/
/*至少发生一次TEAE*/
proc sql;
create table teae_sum as
select  ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by   ACTARM
order by ACTARM;
quit;
/*到SOC*/;
proc sql;
create table teae_sum1 as
select AESOC, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by  AESOC, ACTARM
order by AESOC,ACTARM desc;
quit;
/*到PT*/
proc sql;
create table teae_sum2 as
select AESOC, ACTARM,AEDECOD,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by  AESOC, ACTARM,AEDECOD
order by AESOC,AEDECOD,ACTARM desc;
quit;


/*表14.3.3.2 TEAE按最差严重程度总结*/
/*至少发生一次TEAE*/
proc sql;
create table teae_worst_sum0 as
select ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
where max_ae = AESEVN 
group by ACTARM ;
quit;
proc sql;
create table teae_worst_sum as
select ACTARM,max_ae,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
where max_ae = AESEVN 
group by max_ae,ACTARM;
quit;
/*teae pt最差严重程度*/
proc sql;
create table max_teaept as
select usubjid,AEDECOD,max(aesevn) as max_teaept from adae
group by usubjid,AEDECOD;
quit;
proc sql;
create table union_teaept as
select a.*,b.max_teaept from adae as a
left join max_teaept as b
on a.usubjid = b.usubjid and a.AEDECOD=b.AEDECOD;
quit;
/*到SOC*/
proc sql;
create table teae_worst_sum1 as
select AESOC, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
group by  AESOC,ACTARM 
order by AESOC,ACTARM desc;
quit;
/*到PT*/
proc sql;
create table teae_worst_sum2 as
select AESOC,AEDECOD,AESEVN, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_teaept
where max_teaept = aesevn
group by  AESOC,AEDECOD, AESEVN,ACTARM 
order by AESOC,AEDECOD, AESEVN,ACTARM desc;
quit;
/*不分组*/
proc sql;
create table teae_worst_sum3 as
select AESOC,AESEVN,AEDECOD,count(distinct usubjid) as peop_count,count(*) as case_count from union_ae
group by  AESOC, AESEVN,AEDECOD 
order by AESOC,AEDECOD,AESEVN;
quit;

data worst_teae_sum;
set teae_worst_sum:;
run;


/*表14.3.3.3 TEAE按因果关系总结*/
/*到相关*/
proc sql;
create table teae_relat1 as
select AEREL, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by AEREL,ACTARM
order by AEREL,ACTARM desc;
quit;
/*soc，pt*/
proc sql;
create table teae_relat2 as
select AESOC, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by AESOC,ACTARM
order by AESOC,ACTARM desc;
quit;
/*器官，相关，症状*/
proc sql;
create table teae_relat3 as
select AESOC, AEDECOD,AEREL,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
group by AESOC, AEDECOD,AEREL,ACTARM
order by AESOC, AEDECOD,AEREL,ACTARM desc;
quit;

data relate_teae;
set teae_relat:;
run;


/*表14.3.3.4 药物不良反应总结*/
/*药物不良反应*/
data adr;
set ads.adae;
if AEDRUG = 'Y' and SAFFL = 'Y' and TRTEMFL ='Y' then output;
run;
/*最差严重程度*/;
proc sql;
create table max_adr as
select usubjid,max(aesevn) as max_adr from adr
group by usubjid;
quit;
proc sql;
create table union_adr as
select a.*,b.max_adr from adr as a
left join max_adr as b
on a.usubjid = b.usubjid;
quit;

/*到分组*/
proc sql;
create table teae_med as
select  ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adr
group by  ACTARM
order by ACTARM;
quit;
/*到soc*/
proc sql;
create table teae_med1 as
select AESOC, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adr
group by  AESOC, ACTARM
order by AESOC,ACTARM desc;
quit;
/*到SOC,pt*/
proc sql;
create table teae_med2 as
select AESOC, ACTARM,AEDECOD,count(distinct usubjid) as peop_count,count(*) as case_count from adr
group by  AESOC, ACTARM,AEDECOD
order by AESOC,AEDECOD,ACTARM desc;
quit;

data med_teae;
set teae_med:;
run;


/*表14.3.3.5 药物不良反应按最差严重程度总结*/
/*pt最差严重程度*/;
proc sql;
create table max_adrpt as
select usubjid,AEDECOD,max(aesevn) as max_adrpt from adr
group by usubjid,AEDECOD;
quit;
proc sql;
create table union_adrpt as
select a.*,b.max_adrpt from adr as a
left join max_adrpt as b
on a.usubjid = b.usubjid and a.AEDECOD=b.AEDECOD;
quit;
/*总结*/
proc sql;
create table adr_worst_2 as
select ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_adr
where max_adr = AESEVN 
group by ACTARM;
quit;
/*总结,分级*/
proc sql;
create table adr_worst_1 as
select ACTARM,max_adr,count(distinct usubjid) as peop_count,count(*) as case_count from union_adr
where max_adr = AESEVN 
group by max_adr,ACTARM;
quit;
/*到soc,pt*/
proc sql;
create table adr_worst_sum1 as
select AESOC,AEDECOD, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_adrpt
where max_adrpt = AESEVN 
group by  AESOC,AEDECOD,ACTARM
order by AESOC,AEDECOD,ACTARM desc;
quit;
/*到soc,pt,最差严重程度*/
proc sql;
create table adr_worst_sum2 as
select AESOC,AEDECOD,AESEVN, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from union_adrpt
where max_adrpt = AESEVN 
group by  AESOC,AEDECOD, AESEVN,ACTARM
order by AESOC,AEDECOD,AESEVN,ACTARM desc;
quit;

data worst_adr;
set  adr_worst:;
run;


/*表14.3.3.6 药物不良反应按因果关系总结*/
/*到相关*/
proc sql;
create table adr_relat as
select AEREL, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
where AERELN <=3
group by AEREL,ACTARM
order by AEREL,ACTARM desc;
quit;
/*到soc*/
proc sql;
create table adr_relate1 as
select AESOC,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
where AERELN <=3
group by  AESOC,ACTARM
order by AESOC,ACTARM desc;
quit;
/*soc,pt*/
proc sql;
create table adr_relat2 as
select AESOC,AEDECOD, ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
where AERELN <=3
group by AESOC,AEDECOD,ACTARM
order by AESOC,AEDECOD,ACTARM desc;
quit;
/*soc,pt,相关*/
proc sql;
create table adr_relat3 as
select AESOC,AEDECOD,AEREL,ACTARM,count(distinct usubjid) as peop_count,count(*) as case_count from adae
where AERELN <=3
group by AESOC,AEDECOD,AEREL,ACTARM
order by AESOC,AEDECOD,AEREL,ACTARM desc;
quit;
data relate_adr;
set adr_relat:;
run;


/*表14.3.4.1 实验室检查血生化用药前后各时间点及相比基线变化的情况-丙氨酸氨基转移酶*/
proc sort data=ads.adlb(where=(SAFFL="Y" and LBTEST='丙氨酸氨基转移酶')) out=lbtest_ord1;by AVISITn;run;
ods output means.summary=lbtest1;
proc means data=lbtest_ord1 n mean std median q1 q3 max min;
var aval chg;
class avisitn actarm;
quit;
ods output close;


/*表14.3.4.2 实验室检查血生化用药前后各时间点及相比基线变化的情况-天门冬氨酸氨基转移酶*/
proc sort data=ads.adlb(where=(SAFFL="Y" and LBTEST='天门冬氨酸氨基转移酶')) out=lbtest_ord2;by AVISITn;run;
ods output means.summary=lbtest2;
proc means data=lbtest_ord2 n mean std median q1 q3 max min;
var aval chg;
class avisitn actarm;
quit;
ods output close;


/*表15.1.1.1观察期各采血时间点血药浓度总结*/
data adpc bql;
set ads.adpc;
if PKCSFL='Y' then do;
  if PCCOM='BQL' then output bql;
  else output adpc;
end;
run;
proc sort data=adpc;
by PCPTIMN actarm;
quit;
/*不分组*/
/*几何均数，几何标准差，几何变异系数*/
ods output ConfLimits=geo;
proc ttest data=adpc dist=lognormal;
var PCORRES;
by PCPTIMn;
run;
data geo;
  set geo;
  GeoSD=exp(sqrt(log((CV)**2+1)));
  cv_new=cv*100;
run;
/*算术*/
ods output means.summary=pc_mean;
proc means data=adpc n mean std cv median max min;
var PCORRES;
class PCPTIMn;
quit;
ods output close; 

proc sql;
create table pc_sum as 
select a.*,b.GeomMean,b.GeoSD,b.cv_new from pc_mean as a
inner join geo as b
on a.PCPTIMN=b.PCPTIMN;
quit;

data pc_sum_new;
set pc_sum;
format PCORRES_Min PCORRES_Max 8.2
PCORRES_Mean PCORRES_Median GeomMean 8.3
PCORRES_StdDev PCORRES_cv geosd cv_new 8.4;
run;
/*分组*/
ods output ConfLimits=geo1;
proc ttest data=adpc dist=lognormal;
var PCORRES;
by PCPTIMn actarm;
run;
data geo1;
  set geo1;
  GeoSD=exp(sqrt(log((CV)**2+1)));
  cv_new=cv*100;
run;
/*算术*/
ods output means.summary=pc_mean1;
proc means data=adpc n mean std cv median max min;
var PCORRES;
class PCPTIMn actarm;
quit;
ods output close; 

proc sql;
create table pc_sum1 as 
select a.*,b.GeomMean,b.GeoSD,b.cv_new from pc_mean1 as a
inner join geo1 as b
on a.PCPTIMN=b.PCPTIMN and a.actarm=b.actarm;
quit;

data pc_sum_new1;
set pc_sum1;
format PCORRES_Min PCORRES_Max 8.2
PCORRES_Mean PCORRES_Median GeomMean 8.3
PCORRES_StdDev PCORRES_cv geosd cv_new 8.4;
run;
/*bql*/
proc sql;
create table bql_count as 
select PCPTIMn, ACTARM,count(distinct usubjid) as peop_count from bql
group by PCPTIMn, ACTARM
order by PCPTIMn, ACTARM desc;
quit;


/*表15.1.1.2 观察期血药动力学主要参数情况总结*/
proc sort data=ads.adpp(where=(PKPSFL='Y')) out=adpp;
by param actarm;
quit;
/*几何*/
ods output ConfLimits=pk_geo1;
proc ttest data=adpp dist=lognormal;
var AVAL;
by PARAM;
run;
data pk_geo1;
  set pk_geo1;
  GeoSD=exp(sqrt(log((CV)**2+1)));
  cv_new=cv*100;
run;
/*算术*/
ods output means.summary=pk_mean1;
proc means data=adpp n mean std cv median max min;
var AVAL;
class PARAM;
quit;
ods output close; 

proc sql;
create table pk_sum1 as 
select a.*,b.GeomMean,b.GeoSD,b.cv_new from pk_mean1 as a
inner join pk_geo1 as b
on a.PARAM=b.PARAM;
quit;
data pk_sum_new1;
set pk_sum1;
format aval_Min aval_Max 8.0
aval_Mean aval_Median GeomMean 8.1
aval_StdDev aval_cv geosd cv_new 8.2 ;
run;

/*分组*/
/*几何*/
ods output ConfLimits=pk_geo2;
proc ttest data=adpp dist=lognormal;
var AVAL;
by PARAM actarm;
run;
data pk_geo2;
  set pk_geo2;
  GeoSD=exp(sqrt(log((CV)**2+1)));
  cv_new=cv*100;
run;
/*算术*/
ods output means.summary=pk_mean2;
proc means data=adpp n mean std cv median max min;
var AVAL;
class PARAM actarm;
quit;
ods output close; 

proc sql;
create table pk_sum2 as 
select a.*,b.GeomMean,b.GeoSD,b.cv_new from pk_mean2 as a
inner join pk_geo2 as b
on a.PARAM=b.PARAM and a.actarm=b.actarm;
quit;

data pk_sum_new2;
set pk_sum2;
format aval_Min aval_Max 8.0
aval_Mean aval_Median GeomMean 8.1
aval_StdDev aval_cv geosd cv_new 8.2 ;
run;


/*表15.1.1.3 观察期血药动力学次要参数情况总结*/
data pk_sum_minor1;
set pk_sum1;
format aval_Min aval_Max 8.4
aval_Mean aval_Median GeomMean 8.5
aval_StdDev aval_cv geosd cv_new 8.6 ;
run;
data pk_sum_minor2;
set pk_sum2;
format aval_Min aval_Max 8.4
aval_Mean aval_Median GeomMean 8.5
aval_StdDev aval_cv geosd cv_new 8.6 ;
run;
/*p值*/
/*proc sql;*/
/*create table adpp0 as */
/*select * from adpp*/
/*where  param in ('HL_Lambda_z' 'Vz_obs' 'Lambda_z' 'Cl_obs' 'MRTINF_obs' 'MRTlast' 'Tmax' 'AUC_%Extrap_obs');*/
/*quit;*/
%macro p_value(param=,paramn=);
proc sql;
create table adpp0 as 
select * from adpp
where  param = &param.;
quit;

PROC NPAR1WAY data=adpp0 noprint;
var aval;
exact wilcoxon;
class actarm;
output out=pk_p_&paramn.;
quit;
%mend;
%p_value(param='HL_Lambda_z',paramn=1);
%p_value(param='Vz_obs',paramn=2);
%p_value(param='Lambda_z',paramn=3);
%p_value(param='Cl_obs',paramn=4);
%p_value(param='MRTINF_obs',paramn=5);
%p_value(param='MRTlast',paramn=6);
%p_value(param='Tmax',paramn=7);
%p_value(param='AUC_%Extrap_obs',paramn=8);
data pk_minor_p;
set pk_p_:;
run;
proc sql;
create table pk_pvalue as 
select XP2_WIL from pk_minor_p;
quit;


/*表15.1.1.4 观察期试验组和对照组血药动力学参数生物等效性情况总结*/
data be;
set ads.adpp(where=(PARAM='Cmax' or PARAM='AUClast' or PARAM='AUCINF_obs'));
aval_log=log10(aval);
run;
proc sort data=be;
by param ACTARMN;
quit;
/*90%*/
ods output ConfLimits=be_geo_90;
proc ttest data=be alpha=0.1 dist=lognormal;
var AVAL;
by param;
class actarmn;
run;
ods output close;
/*99.8%*/   
ods output ConfLimits=be_geo_998;
proc ttest data=be alpha=0.002 dist=lognormal;
var AVAL;
by param;
class actarmn;
run;
ods output close;

/*glm求90%*/
ods output lsmeandiffcl=glm_90;
proc glm data=be ;
class actarmn;
model aval_log=actarmn;
lsmeans actarmn/pdiff cl alpha=0.1;
by param;
run;
ods output close;
data means_ratio;
set glm_90;
lower=10**lowercl;
diff_new=10**Difference;
upper=10**uppercl;
run;
/*第二种方法*/
ods output cldiffs=glm_means_90;
proc glm data=be ;
class actarmn;
model aval_log=actarmn;
means actarmn/t cldiff alpha=0.1;
by param;
run;
ods output close;


/*列表16.2.1.1 提前中止研究的受试者*/
proc sql;
create table list_quit as 
select * from ads.adsl
where DCSREASN is not missing;
quit;


/*列表16.2.4.1未入选的受试者*/
proc sql;
create table list_exclude as 
select USUBJID, RFICDT, RANDOMR from ads.adsl
where ARM is missing
order by usubjid;
quit;
 

/*列表16.2.4.2 人口学特征和基线特征*/
proc sql;
create table list_base as 
select USUBJID, ACTARM,sex,age,ETHNIC,ETHNCOTH,HEIGHTBL,weightbl,bmibl,BSABL,RFICDT,SAFFL,PKCSFL,PKPSFL from ads.adsl
where SAFFL='Y'
order by usubjid;
quit;


/*列表16.2.4.3.3 过敏史*/
proc sql;
create table list_allegy as 
select USUBJID, ACTARM from ads.admh
where SAFFL='Y' and MHCAT='过敏史'
order by usubjid;
quit;


/*列表16.2.4.3.4 烟酒史*/
proc sql;
create table list_cigar as 
select USUBJID, ACTARM,SUSMFRQ,SUDRFRQ from ads.adsu
where SAFFL='Y'
order by usubjid;
quit;


/*列表16.2.4.3.5 疫苗接种史*/
proc sql;
create table list_vaccine as 
select USUBJID, ACTARM,MHCAT from ads.admh
where SAFFL='Y' and MHCAT='疫苗接种史'
order by usubjid;
quit;


/*列表16.2.4.3.6 献血失血史*/
proc sql;
create table list_blooddonation as 
select USUBJID, ACTARM,MHCAT from ads.admh
where SAFFL='Y' and MHCAT='献血史|失血史' 
order by usubjid;
quit;

/*列表16.2.4.3.7 手术史*/
proc sql;
create table list_operation as 
select USUBJID, ACTARM,MHCAT,MHTERM,MHSTDTC from ads.admh
where SAFFL='Y' and MHCAT='手术史' 
order by usubjid;
quit;


/*列表16.2.4.4.1 受试者胸部影像学异常结果*/
proc sql;
create table list_lung as 
select USUBJID, ACTARM,AVISIT,ADT,AVALC,PRDESC,ABLFL from ads.adpr
where SAFFL='Y' and PRCAT='胸部影像学检查' and AVALC like '异常%'
order by usubjid;
quit;


/*列表16.2.4.4.2 受试者腹部B超检查异常结果*/
proc sql;
create table list_stomachtest as 
select USUBJID, ACTARM,AVISIT,ADT,AVALC,PRDESC,ABLFL from ads.adpr
where SAFFL='Y' and PRCAT='腹部B超检查' and AVALC like '异常%'
order by usubjid;
quit;


/*列表16.2.4.4.3 受试者尿液药物筛查阳性结果*/
proc sql;
create table list_medurine as 
select USUBJID, ACTARM,AVISIT,PRCAT,ADT,AVALC,ABLFL from ads.adpr
where SAFFL='Y' and PRCAT='尿液药物筛查' and AVALC ='阳性'
order by usubjid;
quit;


/*列表16.2.4.4.4 受试者酒精呼气试验异常结果*/
proc sql;
create table list_alcoholbreath as 
select USUBJID, ACTARM,AVISIT,PRCAT,ADT,AVALC,ABLFL from ads.adpr
where SAFFL='Y' and PRCAT='酒精呼气检查' and AVALC like '异常%'
order by usubjid;
quit;


/*列表16.2.5.1 研究给药记录*/
proc sql;
create table list_medgiven as 
select USUBJID, ACTARM,EXSDT,EXSTTM,EXENTM,DOSEP,DOSEA,DOSER,DOSEU from ads.adex
where SAFFL='Y'
order by usubjid;
quit;


/*列表16.2.5.2 合并用药情况*/
proc sql;
create table list_medcomb as 
select USUBJID, ACTARM,CMTRT,ATC2,CMPTNAM,CMINDC,CMINDCO,CMDESC,CMROUTE,CMDOSE,CMDOSEU,CMDOSFRQ,CMSTDTc,CMENDTc,CMSTAT from ads.adcm
where SAFFL='Y' and CMCAT ='合并用药'
order by usubjid;
quit;


/*列表16.2.6.1 所有不良事件*/
proc sql;
create table list_AE as 
select USUBJID, ACTARM,AETERM,AESOC,AEDECOD,AESTTM,ASTDY,AEOUT,AEENDTC,AENDY,ADURN,AESEVN,AEACN,AEREL,AESER,AEDIS,TRTEMFL,AEDRUG from ads.adae
where SAFFL='Y'
order by usubjid;
quit;


/*列表16.2.6.3 所有药物不良反应*/
proc sql;
create table list_adr as 
select USUBJID, ACTARM,AETERM,AESOC,AEDECOD,AESTTM,ASTDY,AEOUT,AEENDTC,AENDY,ADURN,AESEVN,AEACN,AEREL,AESER,AEDIS,TRTEMFL from ads.adae
where SAFFL='Y' and AEDRUG='Y'
order by usubjid;
quit;


/*列表16.2.6.4 导致提前退出试验的不良事件*/
proc sql;
create table list_ae_out as 
select USUBJID, ACTARM,AETERM,AESOC,AEDECOD,AESTTM,ASTDY,AEOUT,AEENDTC,AENDY,ADURN,AESEVN,AEACN,AEREL,AESER,TRTEMFL,AEDRUG from ads.adae
where SAFFL='Y' and AEDIS='Y'
order by usubjid;
quit;


/*列表16.2.6.5 所有III级及以上TEAE*/
proc sql;
create table list_teae_3 as 
select USUBJID, ACTARM,AETERM,AESOC,AEDECOD,AESTTM,ASTDY,AEOUT,AEENDTC,AENDY,ADURN,AESEVN,AEACN,AEREL,AESER,AEDRUG from ads.adae
where SAFFL='Y' and TRTEMFL='Y' and AESEVN > 3
order by usubjid;
quit;


/*列表16.2.7.1 受试者实验室检查（血常规、尿常规、血生化、凝血功能）异常结果*/
proc sql;
create table list_bloodtest as 
select USUBJID, ACTARM,LBCAT,LBTEST,AVISIT,ADT,LBORRES,LBORRESU,AVALC,ABLFL from ads.adlb
where SAFFL='Y' and (LBCAT='血常规检查' or LBCAT='尿常规检查' or LBCAT='血生化检查' or LBCAT='凝血功能检查' or LBCAT='输血四项') and avalc like '异常%'
order by usubjid,LBCAT,LBTEST;
quit;


/*列表16.2.7.2 受试者12导联心电图检查异常结果*/
proc sql;
create table list_eg as 
select USUBJID, ACTARM,AVISIT,ADT,AVALC,EGDESC,ABLFL from ads.adeg
where SAFFL='Y' and avalc like '异常%'
order by usubjid;
quit;


/*列表16.2.7.3 受试者生命体征异常结果*/
proc sql;
create table list_lifesign as 
select USUBJID, ACTARM,VSTEST,AVISIT,ADT,ATM,VSORRES,VSORRESU,AVALC,ABLFL from ads.advs
where SAFFL='Y' and avalc like '异常%'
order by usubjid;
quit;


/*列表16.2.7.4 受试者体格检查异常结果*/
proc sql;
create table list_physicalexam as 
select USUBJID, ACTARM,PARAM,AVISIT,ADT,AVALC,PEDESC,ABLFL from ads.adpe
where SAFFL='Y' and avalc like '异常%'
order by usubjid;
quit;


/*列表16.2.8.1 受试者血药浓度*/
proc sql;
create table list_pkcs as 
select USUBJID, ACTARM,PCPTIM,EXSDT,EXSTTM,EXENTM,PCDT,PCTIM,PCORRES,PCCOM from ads.adpc
where PKCSFL='Y' 
order by usubjid;
quit;


/*列表16.2.8.2 受试者PK参数*/
proc sql;
create table list_pkps as 
select USUBJID, ACTARM,PARAM,AVAL,UNIT from ads.adpp
where PKPSFL='Y' 
order by usubjid;
quit;


/*图 15.2.1.1 观察期试验组(对照组)个体血药浓度-时间曲线图*/
proc sort data=ads.adpc out=adpc;
by actarm usubjid;
quit;
SYMBOL INTERPOL=JOIN VALUE=DOT;
PROC GPLOT DATA=adpc;
TITLE '观察期试验组个体血药浓度-时间曲线图';
PLOT PCORRES*PCSEQ/LEGEND;
by actarm USUBJID;
RUN;
QUIT;

/*对数曲线*/
data adpc_log;
set adpc;
format PCORRES_log 8.3;
PCORRES_log=log10(PCORRES);
run;

SYMBOL INTERPOL=JOIN VALUE=DOT;
PROC GPLOT DATA=adpc_log;
TITLE '观察期试验组个体血药浓度-时间对数曲线图';
PLOT PCORRES_log*PCSEQ/LEGEND;
by actarm USUBJID;
RUN;
QUIT;


/*图 15.2.1.3 观察期试验组和对照组平均血药浓度-时间曲线图*/
proc sql;
create table adpc_average as
select PCSEQ,ACTARM,mean(PCORRES) as average from ads.adpc
group by actarm,pcseq;
quit;
data adpc_average_log;
set adpc_average;
format average_log 8.3;
average_log=log10(average);
run;

SYMBOL INTERPOL=JOIN VALUE=DOT;
SYMBOL2 INTERPOL=join VALUE='*';
PROC GPLOT DATA=adpc_average;
TITLE '观察期试验组和对照组平均血药浓度-时间曲线图';
PLOT average*PCSEQ=ACTARM/LEGEND ;
RUN;
QUIT;

/*对数曲线图*/
SYMBOL INTERPOL=JOIN VALUE=DOT;
SYMBOL2 INTERPOL=join VALUE=*;
PROC GPLOT DATA=adpc_average_log;
TITLE '观察期试验组和对照组平均血药浓度-时间对数曲线图';
PLOT average_log*PCSEQ=ACTARM/LEGEND ;
RUN;
QUIT;


/*图 15.2.2.1 观察期试验组和对照组血药动力学参数箱式图*/
proc sort data=ads.adpp out=adpp_dummy;
by actarm param;
quit;

proc sgplot data=adpp_dummy(where=(PARAM='Cmax')); 
vbox AVAL;
by actarm;
run;

proc sgplot data=adpp_dummy(where=(PARAM='AUClast')); 
vbox AVAL;
by actarm;
run;

proc sgplot data=adpp_dummy(where=(PARAM='AUCINF_obs')); 
vbox AVAL;
by actarm;
run;


PROC DATASETS LIBRARY=work;
COPY OUT=compare;
QUIT;

 

```





## 参考文献

