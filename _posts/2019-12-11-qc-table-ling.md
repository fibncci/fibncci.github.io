## qc表

```sas
******************Program info***************************************
* Copyright (c)    	        : The pgm codes belong to Knowlands property.
* Project Code/Sponsor Name	: SHR-1314-AS-102;
* Program Name     	        : SHR-1314-AS-102_TFL_compare_0.1.sas
* Purpose          	        : 比对表
* Programmer/Date 	        : XiaoLing 2019.12.6
* Input dataset(s)          : 
* Output			 	    : 
* External macros	used    : null
* SAS Version               : 9.4
********************************************************************;

******************Modification history*******************************
 * Modified by/Date         : Modifier’s name/ MM/DD/YYYY
 * Reason and line          : XXXXXXXXX,XXXXXXXXXX                   
********************************************************************;


libname  ads "E:\SHR-1314-AS-102\3 STATISTICS\Analysis Dataset\ADS_dataset\ADS_dataset";

proc sql;
create table adsl as 
select * from ads.adsl  
order by SUBJID;
quit;

/*表7.1 受试者分布*/




proc sql;
 select count(distinct subjid) from adsl 
 where FILTER='Y';/*筛选	受试者人数*/
quit;
proc sql;
  select ARMA,count(distinct subjid) from adsl 
  where RANDOM='Y'
  group by ARMA;
quit;
proc sql;
  select count(distinct subjid) from adsl 
  where RANDOM='Y';/*随机*/
quit;
proc sql;
  select ARMA,count(distinct subjid) from adsl 
  where TRTSTDT is not missing
  group by ARMA;
quit;
proc sql;
  select count(distinct subjid) from adsl 
  where TRTSTDT is not missing;/**接受研究治疗**/
quit;

proc sql;
  select ARMA,count(distinct subjid) from adsl 
  where ENDSRSN=2
  group by ARMA;
quit;
proc sql;
  select count(distinct subjid) from adsl 
  where ENDSRSN=2;/*完成研究*/
quit;





/*筛选FAS集*/
proc sql;
create table adsl_1 as 
select * from adsl  
where fas='Y'
order by SUBJID;
quit;

proc freq data=adsl_1;
  table ARMA*EXEAR/list sparse;
  where ENDSRSN=1;/*提前退出研究的原因*/
quit;
proc freq data=adsl_1;
  table EXEAR/list sparse;  
  where ENDSRSN=1;/*提前退出研究的原因*/
quit;

/* 表7.2 分析人群*/
%macro sort(var=);
proc freq data=adsl;
  table ARMA*&var./list sparse;
  where &var='Y';
quit;
%mend;
%sort(var=RANDOM);
%sort(var=SAFETY);
%sort(var=FAS);

/*表14.2.3.1 人口学特征(SS)*/
proc sql;
create table adsl_2 as 
select * from adsl  
where SAFETY='Y'
order by SUBJID;
quit;

proc means data=adsl_2 n mean std median min max Q1 Q3 maxdec=2;
 var age heightbl weightbl bmibl ;/*年龄、身高、体重、体重指数*/
run;
proc freq data=adsl_2;
 table sex ethnic /list missing;/*年龄组、性别、民族....*/
quit;
proc sort data=adsl_2;
by ARMA;
run;
proc means data=adsl_2 n mean std median min max Q1 Q3 maxdec=2;
 var age heightbl weightbl bmibl ;/*年龄、身高、体重、体重指数*/
 by ARMA;
run;
proc freq data=adsl_2;
 table sex ethnic /list missing;/*年龄组、性别、民族....*/
 by ARMA;
quit;

/*表14.2.4.1研究药物给药记录*/
proc freq data=adsl;
  table ARMA*MEDNUM/list sparse;
quit;
proc freq data=adsl;
  table MEDNUM/list sparse;
quit;

/*表 14.2.7.1 所有TEAE 发生情况总结(SS)*/
proc sql;
 create table ae1 as
 select a.*,b.* from ads.adae a
 left join ads.adsl b
 on a.subjid=b.subjid
 where  a.SAFETY='Y' and AETRTEFL='E';/*基于 SS & TEAE */
quit;

/*各实际分组情况*/
%macro aet(var=,nam=);
proc sql;
 create table aegp&nam. as 
 select ARMA,count(&var.),'任何TEAE' as label from ae1
 group by ARMA
 union all
 select ARMA,count(&var.),'轻度' as label from ae1 where AETOXGRN=1
 group by ARMA
 union all
 select ARMA,count(&var.),'中度' as label from ae1 where AETOXGRN=2
 group by ARMA
 union all
 select ARMA,count(&var.),'重度' as label from ae1 where AETOXGRN=3
 group by ARMA
 union all
 select ARMA,count(&var.),'严重TEAE' as label from ae1 where AESER='是'
 group by ARMA
 union all
 select ARMA,count(&var.),' 药物不良反应' as label from ae1 where AEDRUG='Y'
 group by ARMA
 union all
 select ARMA,count(&var.),'严重药物不良反应' as label from ae1 where AEDRUG='Y' and AESER='是'
 group by ARMA
 union all
 select ARMA,count(&var.),'转归为死亡的TEAE' as label from ae1 where AEOUT='死亡'
 group by ARMA
 union all
 select ARMA,count(&var.),'导致退出试验的TEAE' as label from ae1 where AEDIS='是'
 group by ARMA
;
quit;
%mend;
%aet(var=distinct subjid,nam=1);
%aet(var=*,nam=2);

/*试验组*/
proc sql;
 create table ae1_1 as
 select * from ae1
 where ARMAN in (2,3,4,5,6);
quit;
%macro aet(var=,nam=);
proc sql;
 create table aesy&nam. as 
 select count(&var.),'任何TEAE' as label from ae1_1
 union all
 select count(&var.),'轻度' as label from ae1_1 where AETOXGRN=1
 union all
 select count(&var.),'中度' as label from ae1_1 where AETOXGRN=2
 union all
 select count(&var.),'重度' as label from ae1_1 where AETOXGRN=3
 union all
 select count(&var.),'严重TEAE' as label from ae1_1 where AESER='是'
 union all
 select count(&var.),' 药物不良反应' as label from ae1_1 where AEDRUG='Y'
 union all
 select count(&var.),'严重药物不良反应' as label from ae1_1 where AEDRUG='Y' and AESER='是'
 union all
 select count(&var.),'转归为死亡的TEAE' as label from ae1_1 where AEOUT='死亡'
 union all
 select count(&var.),'导致退出试验的TEAE' as label from ae1_1 where AEDIS='是'
;
quit;
%mend;
%aet(var=distinct subjid,nam=1);
%aet(var=*,nam=2);


/*表14.2.7.2 治疗期间SAE发生情况总结(SOC和PT，SS)*/
proc sql;
 create table ae2 as
 select * from ae1 
 where AESER='是';
quit;

%macro soc();
proc sql;
 select  count (distinct subjid) from ae2;/*事件发生的例数*/
quit;

proc sql;
 create table ae3 as
 select distinct subjid,AESOCZ,AEDECODZ,ARMA  from ae2 where AEDECODZ is not missing group by subjid,AEDECODZ ;
quit; /*删除重复项、列出受试者编号、身体系统器官主分类中文名称、经字典衍生首选语中文名称*/

proc freq data=ae3 noprint;
 tables ARMA*AESOCZ*AEDECODZ/list out=ae3_1;
run;/*按列排列系统器官分类和首选语，并计算频数*/

proc sql;
 create table ae4 as 
 select distinct subjid,AESOCZ,ARMA from ae2 where AESOCZ is not missing ;
quit;/*列出受试者编号、身体系统器官主分类中文名称*/

proc freq data=ae4 noprint;
 tables ARMA*AESOCZ/list out=ae4_1;
run;/*系统器官分类及各分类频数*/

proc sql;
 create table sae_res as
 select a.*,b.count as count1 from /*a中每列和b中频数*/
  (select ARMA,AESOCZ,"" as AEDECODZ,count from ae4_1 /*从ae4_1中选择器官分类、新建首选语列、器官分类的频数*/
 union all  /*上下连接*/
  select ARMA,AESOCZ,AEDECODZ,count from ae3_1) as a /*从ae3_1中选择器官分类、首选语、每列的频数*/
 left join (select * from ae4_1) as b  /*左右连接  b:器官分类频数*/
 on a.AESOCZ=b.AESOCZ
 group by a.ARMA,a.AESOCZ,a.AEDECODZ;
quit;  /*按系统器官频数降序、首选语频数降序排列*/

%mend;
%soc();

/*表14.3.1.2 所有TEAE按最严重程度分级总结（SOC&PT,SS）  */
/*各试验分组*/
proc sql;
create table max_adrpt1 as
select subjid,max(AETOXGRN) as max_adrpt1 from ae1
group by subjid;
quit;
proc sql;
create table adrpt1 as
select a.*,b.max_adrpt1 from ae1 as a
left join max_adrpt1 as b
on a.subjid = b.subjid;
quit;
proc sql;
 create table adr_1 as 
 select ARMA,count(distinct subjid),max_adrpt1,'至少发生一次TEAE' as label from adrpt1
 group by ARMA,max_adrpt1;
quit;

/*soc最差严重程度*/;
proc sql;
create table max_adrpt2 as
select subjid,AESOCZ,max(AETOXGRN) as max_adrpt2 from ae1
group by subjid,AESOCZ;
quit;
proc sql;
create table adrpt2 as
select a.*,b.max_adrpt2 from ae1 as a
left join max_adrpt2 as b
on a.subjid = b.subjid and a.AESOCZ=b.AESOCZ;
quit;

proc sql;
 create table adr_2_1 as 
 select distinct subjid,AESOCZ,ARMA,max_adrpt2 from adrpt2 where AESOCZ is not missing ;
quit;/*列出受试者编号、身体系统器官主分类中文名称*/

proc freq data=adr_2_1 noprint;
 tables ARMA*AESOCZ*max_adrpt2/list out=adr_2;
run;/*系统器官分类及各分类频数*/

proc sort data=adr_2;
by AESOCZ ARMA ;
run;

/*pt最差严重程度*/;
proc sql;
create table max_adrpt3 as
select subjid,AEDECODZ,max(AETOXGRN) as max_adrpt3 from ae1
group by subjid,AEDECODZ;
quit;
proc sql;
create table adrpt3 as
select a.*,b.max_adrpt3 from ae1 as a
left join max_adrpt3 as b
on a.subjid = b.subjid and a.AEDECODZ=b.AEDECODZ;
quit;

proc sql;
 create table adr_3_1 as
 select distinct subjid,AESOCZ,AEDECODZ,ARMA,max_adrpt3 from adrpt3 where AEDECODZ is not missing ;
quit; /*删除重复项、列出受试者编号、身体系统器官主分类中文名称、经字典衍生首选语中文名称*/

proc freq data=adr_3_1 noprint;
 tables max_adrpt3*ARMA*AESOCZ*AEDECODZ/list out=adr_3;
run;/*按列排列系统器官分类和首选语，并计算频数*/

proc sort data=adr_3;
by AESOCZ  AEDECODZ ARMA;
run;

/*试验组合计*/
/*最差严重程度*/;
proc sql;
create table max_adrpt4 as
select subjid,max(AETOXGRN) as max_adrpt4 from ae1_1
group by subjid;
quit;
proc sql;
create table adrpt4 as
select a.*,b.max_adrpt4 from ae1_1 as a
left join max_adrpt4 as b
on a.subjid = b.subjid;
quit;

proc sql;
 create table adr_4 as 
 select count(distinct subjid),max_adrpt4,'试验组至少发生一次TEAE' as label from adrpt4
 group by max_adrpt4;
quit;

/*soc最差严重程度*/;
proc sql;
create table max_adrpt5 as
select subjid,AESOCZ,max(AETOXGRN) as max_adrpt5 from ae1_1
group by subjid,AESOCZ;
quit;
proc sql;
create table adrpt5 as
select a.*,b.max_adrpt5 from ae1_1 as a
left join max_adrpt5 as b
on a.subjid = b.subjid and a.AESOCZ=b.AESOCZ;
quit;

proc sql;
 create table adr_5_1 as 
 select distinct subjid,AESOCZ,max_adrpt5 from adrpt5 where AESOCZ is not missing ;
quit;/*列出受试者编号、身体系统器官主分类中文名称*/

proc freq data=adr_5_1 noprint;
 tables AESOCZ*max_adrpt5/list out=adr_5;
run;/*系统器官分类及各分类频数*/

proc sort data=adr_5;
by AESOCZ ;
run;

/*pt最差严重程度*/;
proc sql;
create table max_adrpt6 as
select subjid,AEDECODZ,max(AETOXGRN) as max_adrpt6 from ae1_1
group by subjid,AEDECODZ;
quit;
proc sql;
create table adrpt6 as
select a.*,b.max_adrpt6 from ae1_1 as a
left join max_adrpt6 as b
on a.subjid = b.subjid and a.AEDECODZ=b.AEDECODZ;
quit;

proc sql;
 create table adr_6_1 as
 select distinct subjid,AESOCZ,AEDECODZ,max_adrpt6 from adrpt6 where AEDECODZ is not missing ;
quit; /*删除重复项、列出受试者编号、身体系统器官主分类中文名称、经字典衍生首选语中文名称*/

proc freq data=adr_6_1 noprint;
 tables max_adrpt6*AESOCZ*AEDECODZ/list out=adr_6;
run;/*按列排列系统器官分类和首选语，并计算频数*/

proc sort data=adr_6;
by AESOCZ  AEDECODZ ;
run;


/*表14.2.7.4 所有治疗期间药物不良反应总结（SOC和PT，SS）  */
proc sql;
 create table ae3 as
 select * from ae1 
 where AEDRUG='Y';
quit;

/*各试验分组*/
proc sql;
 create table adur_1 as 
 select ARMA,count(distinct subjid),AEREL,'至少发生一次TEAE' as label from ae3
 group by ARMA,AEREL;
quit;

/*SOC*/
proc sql;
 create table adur_2_1 as 
 select distinct subjid,AESOCZ,ARMA,AEREL from ae3 where AESOCZ is not missing ;
quit;/*列出受试者编号、身体系统器官主分类中文名称*/

proc freq data=adur_2_1 noprint;
 tables ARMA*AESOCZ*AEREL/list out=adur_2;
run;/*系统器官分类及各分类频数*/

proc sort data=adur_2;
by AESOCZ ARMA ;
run;

/*PT*/
proc sql;
 create table adur_3_1 as
 select distinct subjid,AESOCZ,AEDECODZ,ARMA,AEREL from ae3 where AEDECODZ is not missing ;
quit; /*删除重复项、列出受试者编号、身体系统器官主分类中文名称、经字典衍生首选语中文名称*/

proc freq data=adur_3_1 noprint;
 tables AEREL*ARMA*AESOCZ*AEDECODZ/list out=adur_3;
run;/*按列排列系统器官分类和首选语，并计算频数*/

proc sort data=adur_3;
by AESOCZ AEDECODZ ARMA;
run;

proc sql;
 create table ae3_1 as
 select * from ae3 
 where ARMAN in (2,3,4,5,6);
quit;

/*.....*/

/*表14.2.8.1.1-表14.2.8.4 各时间点及相比基线变化的情况*/
%macro lbcomp(name=,var=);
proc sql;
 create table &var. as
 select a.*,b.* from ads.adlb a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.safety='Y' and LBCAT=&name.;
quit;   
proc means data=&var. n mean std median min max maxdec=3 ;
 var LBSTRESN ;
 class LBTEST;
 where LBBLFL="Y";/*基线的结果*/
run;
proc means data=&var. n mean std median min max maxdec=3 ;
 var LBSTRESN LBBLCHG;  /*各访视期结果和相对基线变化*/
 class LBTEST VISIT ;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

proc means data=&var. n mean std median min max maxdec=3 ;
 var LBSTRESN ;
 class LBTEST ARMA;
 where LBBLFL="Y";/*基线的结果*/
run;
proc means data=&var. n mean std median min max maxdec=3 ;
 var LBSTRESN LBBLCHG;  /*各访视期结果和相对基线变化*/
 class LBTEST VISIT ARMA;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;
%mend;
%lbcomp(name='血常规',var=xcg);
%lbcomp(name='血生化',var=xsh);
%lbcomp(name='C反应蛋白',var=cdb);
%lbcomp(name='血沉',var=xc);

/*表14.2.8.5-表14.2.8.9 临床意义交叉变化表*/
%macro lbyycomp(name=,var=);
proc sql;
 create table &var. as
 select a.*,b.* from ads.adlb a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.safety='Y' and LBCAT=&name. and VISITNUM not in(1,2,15);
quit;        /*基于 SS  & 在治疗期和治疗后*/
proc freq data=&var. noprint;
 tables lbtest*ARMA*visit*visitnum*LBBLPCSA*LBPCSA/ list out=re_&var. ;
run;   /*建立列表格，按检查项、访视名称、分析状况和基线状况分别列出频数和百分比*/
proc sort data=re_&var.;
 by lbtest ARMA visitnum;  /*先按检查项排序、再按访视名称排序*/
run;
%mend;
%lbyycomp(name='血常规',var=xcgyy);
%lbyycomp(name='血生化',var=xshyy);
%lbyycomp(name='C反应蛋白',var=cdbyy);
%lbyycomp(name='血沉',var=xcyy);
%lbyycomp(name='尿常规',var=ncgyy);

/*表14.2.9.1-表14.2.9.5 生命体征相比基线变化*/
proc sql;
 create table vs as
 select a.*,b.* from ads.advs a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.safety='Y';
quit;   
proc means data=vs n mean std median min max maxdec=3 ;
 var VSBLRES ;
 class VSTEST;
 where VSBLFL="Y";/*基线的结果*/
run;
proc means data=vs n mean std median min max maxdec=3 ;
 var VSORRES VSBLCHG;  /*各访视期结果和相对基线变化*/
 class VSTEST VISIT ;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

proc means data=vs n mean std median min max maxdec=3 ;
 var VSBLRES ;
 class VSTEST ARMA;
 where VSBLFL="Y";/*基线的结果*/
run;
proc means data=vs n mean std median min max maxdec=3 ;
 var VSORRES VSBLCHG;  /*各访视期结果和相对基线变化*/
 class VSTEST VISIT ARMA ;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

/*表14.2.10.1-表14.2.10.5 心电图相比基线变化*/
proc sql;
 create table eg as
 select a.*,b.* from ads.adeg a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.safety='Y';
quit;   
proc means data=eg n mean std median min max maxdec=3 ;
 var EGSTRESN ;
 class EGTEST;
 where EGBLFL="Y";/*基线的结果*/
run;
proc means data=eg n mean std median min max maxdec=3 ;
 var EGSTRESN EGBLCHG;  /*各访视期结果和相对基线变化*/
 class EGTEST VISIT ;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

proc means data=eg n mean std median min max maxdec=3 ;
 var EGSTRESN ;
 class EGTEST ARMA;
 where EGBLFL="Y";/*基线的结果*/
run;
proc means data=eg n mean std median min max maxdec=3 ;
 var EGSTRESN EGBLCHG;  /*各访视期结果和相对基线变化*/
 class EGTEST VISIT ARMA;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

/*表14.2.11 治疗期和随访期12导联心电图临床意义交叉变化表（SS）*/
proc sql;
 create table egyy as
 select a.*,b.* from ads.adeg a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.safety='Y' and VISITNUM not in(1,2,15) and EGTEST='总体情况';
quit;        /*基于 SS  & 在治疗期和治疗后*/
proc freq data=egyy noprint;
 tables ARMA*visit*visitnum*EGBLRESC*EGSTRESC/ list out=re_egyy ;
run;   /*建立列表格，按检查项、访视名称、分析状况和基线状况分别列出频数和百分比*/
proc sort data=re_egyy;
 by ARMA visitnum;  /*先按检查项排序、再按访视名称排序*/
run;

/*表14.2.16.1-表14.2.16.2*/
%macro ASAS(nam=);
proc sql;
 create table nrs_&nam. as
 select distinct a.subjid,a.NRSAS&nam.,a.VISIT,b.ARMA from ads.adnrs a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.fas='Y' and VISITNUM not in(1,2,15) and NRSAS&nam.='Y';
quit;
 
proc freq data=nrs_&nam. noprint;
 tables ARMA*visit/ list out=re_nrs_&nam. ;
run;   
%mend;
%ASAS(nam=20);
%ASAS(nam=40);

/*表14.2.16.3-表14.2.16.9 各评分相比基线变化*/
proc sql;
 create table nrs as
 select a.*,b.* from ads.adnrs a
 left join ads.adsl b
 on a.subjid=b.subjid
 where a.fas='Y';
quit;   
proc means data=nrs n mean std median min max maxdec=3 ;
 var NRSBLRES ;
 class NRSTEST;
 where NRSBLFL="Y";/*基线的结果*/
run;
proc means data=nrs n mean std median min max maxdec=3 ;
 var NRSORRES NRSBLCHG;  /*各访视期结果和相对基线变化*/
 class NRSTEST VISIT ;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;

proc means data=nrs n mean std median min max maxdec=3 ;
 var NRSBLRES ;
 class NRSTEST ARMA;
 where NRSBLFL="Y";/*基线的结果*/
run;
proc means data=nrs n mean std median min max maxdec=3 ;
 var NRSORRES NRSBLCHG;  /*各访视期结果和相对基线变化*/
 class NRSTEST VISIT ARMA;  /*按检查项和访视期分类*/
 where VISITNUM not in(1,2,15);  /*除筛选期和计划外访视*/
run;



```

## 参考文献











