---
layout: post
title: "qc表"
date: 2019-12-16
tag: sas
---





qc表



```sas


libname  ads "E:\SHR-1314-AS-102\3 STATISTICS\Analysis Dataset\ADS_dataset\ADS_dataset";

proc sql;
	create table df2.adsl as 
	select * from ads.adsl  
	order by SUBJID;
quit;


表7.1 受试者分布 	



/*筛选人数总和  78条数据*/
proc sql;
	create table df2.adsl71aa as 
	select count(distinct subjid) from df2.adsl 
	where FILTER='Y';
quit;


/*随机人数 总和，然后按照 实际分组 分个数 */
proc sql;
	create  table  df2.adsl71bb as
	select ARMA,count(distinct subjid) from df2.adsl 
	where RANDOM='Y'
	group by ARMA;
quit;

/*随机人数的总和*/
proc sql;
	create  table  df2.adsl71cc as
	select count(distinct subjid) from df2.adsl 
	where RANDOM='Y';
quit;



/*研究治疗开始日期 总和，然后按照 实际分组 分个数 */

proc sql;
	create  table  df2.adsl71dd as
	select ARMA,count(distinct subjid) from df2.adsl
	where TRTSTDT is not missing
/*	where TRTSTDT is not NULL*/
	group by ARMA;
quit;



/*研究治疗开始日期 总和-接受研究治疗  */

proc sql;
	create  table  df2.adsl71ef as
	select count(distinct subjid) from df2.adsl
	where TRTSTDT is not missing;
/*	where TRTSTDT is not NULL*/
quit;


/*研究结束原因编号 总和 ,然后治疗分组编号 */

proc sql;
	create table df2.adsl71sss as 
  	select ARMA,count(distinct subjid) from df2.adsl 
  	where ENDSRSN=2
  	group by ARMA;
quit;

/*完成研究 - 35*/
proc sql;
	create table df2.adsl71zz as 
	select count(distinct subjid) from df2.adsl 
	where ENDSRSN=2;
quit;

/*筛选FAS 集合---不知道想看什么东西*/

proc sql;
	create table df2.adsl71zzz as
	select * from df2.adsl 
	where fas = "Y"
	order by subjid;
quit;


/*提前退出研究的原因*/
proc freq data = df2.adsl71zzz ;
/*	create table df2.adsl71zzza as*/
	table arma * exear/list sparse;
	where endsrsn = 1;
quit;



/*提前退出研究的原因 2行5列*/
proc freq data= df2.adsl71zzz;
/*	create table df2.adsl71zzzb as  不可能加*/
	 table   EXEAR/list sparse;  
	where ENDSRSN=1;
quit;


/*提前退出研究的原因 2行5列     freq 频数   sparse 稀疏的 */
proc freq data=adsl_1;
  table ARMA*EXEAR/list sparse;
  where ENDSRSN=1;
quit;

表7.2 分析人群 	

/*貌似第一句没啥用*/
%macro sort(var=);
proc freq data=df2.adsl;
  table ARMA*&var./list sparse;
  where &var='Y';
quit;
%mend;
%sort(var=RANDOM);
%sort(var=SAFETY);
%sort(var=FAS);






表14.2.3.1 人口学特征(SS) 	


proc sql;
create table adsl_2 as 
select * from df2.adsl  
where SAFETY='Y'
order by SUBJID;
quit;

/* median 中位数 ;mean 平均的  最大值*/
/*年龄、身高、体重、体重指数*/
proc means data=adsl_2 n mean std median min max Q1 Q3 maxdec=2;
 var age heightbl weightbl bmibl ;
run;



/*年龄组、性别、民族....*/
proc freq data=adsl_2;
 table sex ethnic /list missing;
quit;
proc sort data=adsl_2;
by ARMA;
run;


/*年龄、身高、体重、体重指数*/
proc means data=adsl_2 n mean std median min max Q1 Q3 maxdec=2;
 var age heightbl weightbl bmibl ;
 by ARMA;
run;

/*年龄组、性别、民族....*/
proc freq data=adsl_2;
 table sex ethnic /list missing;
 by ARMA;
quit;



表14.2.4.1研究药物给药记录 	

表14.2.7.1 所有TEAE发生情况总结(SS) 	

表14.2.7.2 治疗期间SAE发生情况总结(SOC和PT，SS) 	

表14.2.7.3 TEAE按最严重程度总结（SOC和PT，SS） 	

表14.2.7.4 所有治疗期间药物不良反应总结（SOC和PT，SS） 	

表14.2.8.1.1 治疗期和随访期血常规各时间点及相比基线变化的情况-白细胞计数（10^9/L，SS） 	

表14.2.8.1.2 治疗期和随访期血常规各时间点及相比基线变化的情况-红细胞计数（10^12/L，SS） 	

表14.2.8.1.3 治疗期和随访期血常规各时间点及相比基线变化的情况-血红蛋白（g/L，SS） 	

表14.2.8.1.4 治疗期和随访期血常规各时间点及相比基线变化的情况-红细胞压积（L/L，SS） 	

表14.2.8.1.5 治疗期和随访期血常规各时间点及相比基线变化的情况-淋巴细胞百分率（%，SS） 	

表14.2.8.1.6 治疗期和随访期血常规各时间点及相比基线变化的情况-中性粒细胞百分率（%，SS） 	

表14.2.8.1.7 治疗期和随访期血常规各时间点及相比基线变化的情况-单核细胞百分率（%，SS） 	

表14.2.8.1.8 治疗期和随访期血常规各时间点及相比基线变化的情况-嗜酸性粒细胞百分率（%，SS） 	

表14.2.8.1.9 治疗期和随访期血常规各时间点及相比基线变化的情况-嗜碱性粒细胞百分率（%，SS） 	

表14.2.8.1.10 治疗期和随访期血常规各时间点及相比基线变化的情况-淋巴细胞计数（10^9/L，SS） 	

表14.2.8.1.11 治疗期和随访期血常规各时间点及相比基线变化的情况-中性粒细胞计数（10^9/L，SS） 	

表14.2.8.1.12 治疗期和随访期血常规各时间点及相比基线变化的情况-单核细胞计数（10^9/L，SS） 	

表14.2.8.1.13 治疗期和随访期血常规各时间点及相比基线变化的情况-嗜酸性粒细胞计数（10^9/L，SS） 	

表14.2.8.1.14 治疗期和随访期血常规各时间点及相比基线变化的情况-嗜碱性粒细胞计数（10^9/L，SS） 	

表14.2.8.2.1 治疗期和随访期血生化各时间点及相比基线变化的情况-谷草转氨酶（U/L，SS） 	

表14.2.8.2.2 治疗期和随访期血生化各时间点及相比基线变化的情况-谷丙转氨酶（U/L，SS） 	

表14.2.8.2.3 治疗期和随访期血生化各时间点及相比基线变化的情况-碱性磷酸酶(U/L，SS） 	

表14.2.8.2.4 治疗期和随访期血生化各时间点及相比基线变化的情况-乳酸脱氢酶(U/L，SS） 	

表14.2.8.2.5 治疗期和随访期血生化各时间点及相比基线变化的情况-总胆红素(μmol/L，SS） 	

表14.2.8.2.6 治疗期和随访期血生化各时间点及相比基线变化的情况-总蛋白(g/L，SS） 	

表14.2.8.2.7 治疗期和随访期血生化各时间点及相比基线变化的情况-白蛋白(g/L，SS） 	

表14.2.8.2.8 治疗期和随访期血生化各时间点及相比基线变化的情况-甘油三脂(mmol/L，SS） 	

表14.2.8.2.9 治疗期和随访期血生化各时间点及相比基线变化的情况-胆固醇(mmol/L，SS） 	

表14.2.8.2.10 治疗期和随访期血生化各时间点及相比基线变化的情况-高密度脂蛋白胆固醇(mmol/L，SS） 	

表14.2.8.2.11 治疗期和随访期血生化各时间点及相比基线变化的情况-低密度脂蛋白胆固醇(mmol/L，SS） 	

表14.2.8.2.12 治疗期和随访期血生化各时间点及相比基线变化的情况-尿酸(μmol/L，SS） 	

表14.2.8.2.13 治疗期和随访期血生化各时间点及相比基线变化的情况-钠(mmol/L，SS） 	

表14.2.8.2.14 治疗期和随访期血生化各时间点及相比基线变化的情况-钾(mmol/L，SS） 	

表14.2.8.2.15 治疗期和随访期血生化各时间点及相比基线变化的情况-氯(mmol/L，SS） 	

表14.2.8.2.16 治疗期和随访期血生化各时间点及相比基线变化的情况-钙(mmol/L，SS） 	

表14.2.8.2.17 治疗期和随访期血生化各时间点及相比基线变化的情况-磷(mmol/L，SS） 	

表14.2.8.2.18 治疗期和随访期血生化各时间点及相比基线变化的情况-镁(mmol/L，SS） 	

表14.2.8.2.19 治疗期和随访期血生化各时间点及相比基线变化的情况-尿素(mmol/L，SS） 	

表14.2.8.2.20 治疗期和随访期血生化各时间点及相比基线变化的情况-肌酐(μmol/L，SS） 	

表14.2.8.2.21 治疗期和随访期血生化各时间点及相比基线变化的情况-葡萄糖(mmol/L，SS） 	

表14.2.8.3 治疗期和随访期C反应蛋白各时间点及相比基线变化的情况 (mg/L，SS） 	

表14.2.8.4 治疗期和随访期血沉各时间点及相比基线变化的情况 (mm/h ，SS） 	

表14.2.8.5治疗期和随访期血常规临床意义交叉变化表（SS） 	

表14.2.8.6 治疗期和随访期尿常规临床意义交叉变化表（SS） 	

表14.2.8.7治疗期和随访期血生化临床意义交叉变化表（SS） 	

表14.2.8.8 治疗期和随访期C反应蛋白临床意义交叉变化表（SS） 	

表14.2.8.9 治疗期和随访期血沉临床意义交叉变化表（SS） 	

表14.2.9.1 治疗期和随访期生命体征各时间点及相比基线变化的情况-脉搏（次/min，SS） 	

表14.2.9.2 治疗期和随访期生命体征各时间点及相比基线变化的情况-呼吸频率（次/min，SS） 	

表14.2.9.3 治疗期和随访期生命体征各时间点及相比基线变化的情况-收缩压（mmHg，SS） 	

表14.2.9.4 治疗期和随访期生命体征各时间点及相比基线变化的情况-舒张压（mmHg，SS） 	

表14.2.9.5 治疗期和随访期生命体征各时间点及相比基线变化的情况-体温（℃，SS） 	

表14.2.10.1 治疗期和随访期12导联心电图各时间点及相比基线变化的情况-心率（次/分，SS） 	

表14.2.10.2 治疗期和随访期12导联心电图各时间点及相比基线变化的情况-PR间期（ms，SS） 	

表14.2.10.3 治疗期和随访期12导联心电图各时间点及相比基线变化的情况-QT间期（ms，SS） 	

表14.2.10.4 治疗期和随访期12导联心电图各时间点及相比基线变化的情况-QRS间期（ms，SS） 	

表14.2.10.5 治疗期和随访期12导联心电图各时间点及相比基线变化的情况-QTcF间期（ms，SS） 	

表14.2.11 治疗期和随访期12导联心电图临床意义交叉变化表（SS） 	

表14.2.16.1治疗期和随访期各时间点ASAS20应答受试者情况总结（FAS） 	

表14.2.16.2治疗期和随访期各时间点ASAS40应答受试者情况总结（FAS） 	

表14.2.16.3治疗期和随访期患者自我评分NRS各时间点及相比基线变化的情况（FAS） 	

表14.2.16.4治疗期和随访期患者医生对患者评分NRS各时间点及相比基线变化的情况（FAS） 	

表14.2.16.5治疗期和随访期BASFI评分各时间点及相比基线变化的情况（FAS） 	

表14.2.16.6治疗期和随访期BASDAI评分各时间点及相比基线变化的情况（FAS） 	

表14.2.16.7治疗期和随访期BASMI评分各时间点及相比基线变化的情况（FAS） 	

表14.2.16.8治疗期和随访期ASDAS-CRP评分各时间点及相比基线变化的情况（FAS） 	

表14.2.16.9治疗期和随访期ASDAS-ESR评分各时间点及相比基线变化的情况（FAS） 	

列表14.2.2.1 筛选失败的受试者 	

列表14.2.2.2 提前退出研究的受试者 	

列表14.2.3.2 人口学特征和基线特征 	

列表14.2.3.3 吸烟饮酒史 	

列表14.2.3.4过敏史 	

列表14.2.3.5 中轴型脊柱关节炎病史及诊断 	

列表14.2.3.6既往病史（除AxSpA） 	

列表14.2.3.7 药物治疗史 	

列表14.2.3.8 非药物治疗史（除手术史） 	

列表14.2.3.9 手术史 	

列表14.2.3.10 eGFR（MDRD） 	

列表14.2.3.11 γ干扰素释放试验 	

列表14.2.3.12 传染病筛查 	

列表14.2.3.13 胸部X线 	

列表14.2.4.2研究药物给药记录 	

列表14.2.4.3 合并用药情况 	

列表14.2.4.4 合并非药物治疗 	

列表14.2.12.1 所有不良事件 	

列表14.2.12.2 所有严重不良事件 	

列表14.2.12.3 所有药物不良反应 	

列表14.2.12.4 导致退出试验的不良事件 	

列表14.2.13.1 实验室检查（血常规、尿常规、血生化）结果异常的受试者 	

列表14.2.13.2 C反应蛋白检查的受试者 	

列表14.2.13.3 血沉检查的受试者 	

列表14.2.13.4尿妊娠检查阳性的受试者 	

列表14.2.13.5血妊娠试验（育龄女性）的受试者 	

列表14.2.13.6实验室检查（凝血常规）结果异常的受试者 	

列表14.2.14 12导联心电图检查异常的受试者 	

列表14.2.15 体格检查异常的受试者 	

列表14.2.16 有注射部位反应的受试者 	

```

