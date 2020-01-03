---
layout: post
title: "sas-函数"
date: 2019-12-10
tag: sas
---



## 函数

## 字符函数

| 1.字符函数                                                   |                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Anyalnum(参数，n)                                            | *从n开始计算出现第一个字符或者数字的位置是多少*/             | a='321 abc';      b=anyalnum(a,3);/*  结果：b=3*/            |
| ANYALPHA(arg,start)：                                        | 返回第一次出现任意字母的位置，可选开始位置start。            |                                                              |
| ANYDIGIT(arg,start)：                                        | 返回第一次出现任意数字的位置，可选开始位置start。            |                                                              |
| ANYSPACE(arg,start)：                                        | 返回第一次出现任意空白的位置，可选开始位置start。            |                                                              |
| BYTE(n)                                                      | 返回ASCII码值为n所对应的字符                                 |                                                              |
| COLLATE(X,Y)                                                 | 返回ASCII码起始位置为X，终止位置为Y之间所有的字符            | data _null_;      x=collate(48,,10);      y=collate(48,57);      put @1 x @14 y;      run; |
| Cat(arg1,arg2,....argn)                                      | 连接字符串并且保留原来字符串之间的空格                       | data _null_;      a='  Dog';      b='Cat  ';      c='Pig ';      R_cat=cat(a,b,c);      R_cats=cats(a,b,c);      R_catx1=catx('&',a,b,c);      R_catx2=catx('@',a,b,c);      put R_cat=      R_cats=      R_catx1=      R_catx2=      ;      run;      结果：      R_cat=DogCat  Pig       R_cats=DogCatPig       R_catx1=Dog&Cat&Pig       R_catx2=Dog@Cat@Pig |
| Cats(agr1,arg2,...,argn)                                     | 连接字符串并且去掉原来字符之间的空格                         |                                                              |
| Catx('separator-sign',arg1,arg2,...,argn)                    | 连接字符串去掉字符串间的空格增加设定的连接符                 |                                                              |
| CHAR(string,   position)                                     |                                                              | options pageno=1 ps=64 ls=80   nodate;            data test;         retain string   "abc";         do position = -1 to 4;            result=char(string,   position);            output;         end;      run;            proc print noobs data=test;      run; |
| COALESCEC Function                                           |                                                              |                                                              |
| COMPRESS(<source><,   chars><, modifiers>)                   | 压缩字符串移除字符串中指定的符号默认移除空格                 | data _null_;      a='  Dog  &cat ';      R1=compress(a);      R2=compress(a,'&');      put R1=      R2=      ;      run;             结果：      R1=Dog&cat R2=Dog  cat            data _null_;      x='123-4567-8901 B 234-5678-9012 c';      y=compress(x,'ABCD','k');      put y;      run; |
| COMPBL(X)                                                    | 把字符串X中多余空格去掉，即将连续多个空格压缩为一个          |                                                              |
| COUNT(string,substring<,modifiers>)                          |                                                              | xyz='This is a thistle? Yes,   this is a thistle.';      howmanythis=count(xyz,'this');      put howmanythis;            data _null_;      expression1='This is a thistle? '\|\|'Yes, this is a thistle.';      expression2=kscan('This is',2)\|\|'       ';      expression3=compress('i     '\|\|'  t    ');      howmanyis_it=count(expression1,expression2,expression3);      put howmanyis_it expression2 ;            run; |
| COUNTC(string,characters<,modifiers>)                        |                                                              | data _null_;      do i=1 to 3 by 1;      xyz='Baboons Eat Bananas     ';      characters='b';      if i=2 then characters='f';      howmanyb=countc(xyz,characters,'i');      put howmanyb;      end;      run; |
| COUNTW(<string><, chars><, modifiers>)                       |                                                              | options ls=64 pageno=1   nodate;      data test;         length default blanks mp 8;         input string $char60.;         default = countw(string);         blanks = countw(string, '   ');         mp = countw(string, 'mp');         datalines;      中国人 好              Leading blanks      2+2=4      /unix/path/names/use/slashes      \Windows\Path\Names\Use\Backslashes      ;      run;            proc print noobs data=test;      run; |
| dequote                                                      |                                                              | data test;         input string $60.;         result = dequote(string);         datalines;      No quotes, no change      No "leading" quote, no change      "" returns a string with length zero      "Matching double quotes are removed"      'Matching single quotes are removed'      "Paired ""quotes"" are reduced"      'Paired '' quotes'' are reduced'      "Single 'quotes' inside '' double'' quotes are unchanged"      'Double "quotes" inside ""single"" quotes are   unchanged'      "No matching quote, no problem      Don't remove this apostrophe      "Text after the matching quote" is "deleted"      "Text after the matching quote"" is   "deleted"      ;            proc print noobs;      title 'Input Strings and Output Results from DEQUOTE';      run; |
| FIND(string,substring<,modifiers><,startpos>)                |                                                              | data test;      xyz='She sells seashells? Yes, she does.';      z=length(xyz);      startposexp=1-23;      whereisShe_ineg22=find(xyz,'She','i',startposexp);      put z whereisShe_ineg22;            run; |
| FINDC(string,characters<,modifiers><,startpos>)              |                                                              | data _null_;         whereishi=0;         do until(whereishi=0);            whereishi=findc('Hi there,   Ian!','hi ',whereishi+1);            if whereishi=0 then put   "The End";            else do;               whatfound=substr('Hi there,   Ian!',whereishi,1);               put whereishi=   whatfound=;            end;         end;      run; |
| FIRST(string)                                                |                                                              | options pageno=1 ps=64 ls=80   nodate;            data test;         retain string   "abc";         do position = -1 to 4;            result=char(string,   position);            output;         end;      run;            proc print noobs data=test;      run; |
| IFC(logical-expression,   value-returned-when-true, value-returned-when-false   <,value-returned-when-missing>) | data _null_;         input name $ grade;         performance = ifc(grade>80,   'Pass             ', 'Needs   Improvement');         put name= performance=;         datalines;      John 74      Kareem 89      Kati 100      Maria 92      ;            run; |                                                              |
| IFN(logical-expression,   value-returned-when-true, value-returned-when-false   <,value-returned-when-missing>) | data _null_;         input TotalSales;         commission=ifn(TotalSales >   10000, TotalSales*.05, TotalSales*.02);         put commission=;         datalines;      25000      10000      500      10300      ;            run; |                                                              |
| KSCAN(argument,n<,   delimiters>)                            |                                                              |                                                              |
| length(str)                                                  | 返回指定字符串的长度 字符串尾部的空格不计算在内              | data _null_;      a='Dogcat';      b=' Dog cat';      c=' Dog cat   ';      Ra=length(a);      Rb=length(b);      Rc=length(c);      put Ra=      Rb=      Rc=      ;      run;             结果：      Ra=6 Rb=8 Rc=8 |
| Substr(str,n,m)                                              | 从位置n开始从字符串中提取m个字符                             |                                                              |
| Translate(string,to,from,<,...to-n,from-n>)                  | 变换字符串中字符的顺序，或者替换字符。                       | Eg:      data _null_;      A='8/14/2010';      B=translate(a,'-','/');      put      B=      ;      run;      结果：      B=8-14-2010 |
| Tranwrd(str,’from’,’to’)                                     | 将字符串中的某些字符替换为其他字符。                         | Eg:      data _null_;      A='dog cat';      B=tranwrd(a,'cat','pig');      put;      B=      ;      run;      结果：      B=dog pig |
| PROPCASE(arg)                                                | 首字母大写。                                                 |                                                              |
| TRIM(arg)：                                                  | 删除尾部空白。                                               |                                                              |
| UPCASE(arg)：                                                | 替换成大写。                                                 |                                                              |
| REPEAT(s,n)                                                  | 字符表达式s重复n次。                                         |                                                              |
| INPUT(source, <?   \| ??>informat.)                          | input函数可以将字符型变量转换为字符型或数值型，这取决于指定的输入格式informat；而inputn函数只能将字符型变量转换为数值型。从这个角度上看，跟inputc函数一样，可以将inputn函数的功能理解为input函数功能的子集。 | numdate=122591;      chardate=put(numdate,z6.);      sasdate=input(chardate,mmddyy6.); |
| PUT(source,   format.)                                       | 数值型转换成字符型                                           | cchex=put(cc,hex4.);将数字变量CC转换为4个字节的hexadecimal格式 |
| SCAN(string ,n<, delimiter(s)>)                              | char是分隔符，i是取第几部分                                  | data work.test;      Title = 'A Tale of two Cities, Charles j.Dickens';      Word = scan(title,3,'t');      put word= ;      run;      结果是 of |
| NLITERAL(string)                                             | 将字符转为化sas格式                                          | data test;         input string $32.;         length result $ 67;         result = nliteral(string);         datalines;      abc_123      This and That      cats & dogs      Company's profits (%)      "Double Quotes"      'Single Quotes'      ;            proc print;      title 'Strings Converted to N-Literals or Returned Unchanged';      run;            Converting Strings to Name Literals with NLITERAL                         Strings Converted to   N-Literals or Returned Unchanged              1                      Obs    string                   result                       1     abc_123                  abc_123                                   2     This and That            "This and That"N                          3     cats & dogs              'cats & dogs'N                            4     Company's profits (%)    'Company''s profits (%)'N                 5     "Double Quotes"          '"Double Quotes"'N                        6     'Single Quotes'          "'Single Quotes'"N |
| NOTDIGIT(string <,start>)                                    | 返回字符串中第一个不是数字的字符的位置，起始位置可选         | data _null_;         string='Next = _n_ + 12E3;';            j=0;         do until(j=0);            j=notdigit(string,j+1);            if j=0 then put +3 "That's   all";            else do;               c=substr(string,j,1);               put +3 j= c=;            end;         end;      run;            The following lines are written to the SAS log:                j=1 c=N         j=2 c=e         j=3 c=x         j=4 c=t         j=5 c=          j=6 c==         j=7 c=          j=8 c=_         j=9 c=n         j=10 c=_         j=11 c=          j=12 c=+         j=13 c=          j=16 c=E         j=18 c=;         That's all |
| NOTLOWER(string <,start>)                                    | 返回字符串中第一个不是小写字符的位置，起始位置可选           | data _null_;             string='Next = _n_ + 12E3;';           j=0;           do until(j=0);              j=notlower(string,j+1);              if j=0 then put +3 "That's   all";              else do;                         c=substr(string,j,1);                 put +3 j= c=;              end;          end;      run;            The following lines are written to the SAS log:                j=1 c=N         j=5 c=          j=6 c==         j=7 c=          j=8 c=_         j=10 c=_         j=11 c=          j=12 c=+         j=13 c=          j=14 c=1         j=15 c=2         j=16 c=E         j=17 c=3         j=18 c=;         That's all |
| propcase(argument <,delimiter(s)>)                           | 将所有的字母转化为适当的形式，也就是都是小写，除了空格和/等分隔符之后的第一个字母大写，也可以自定义分隔符 | data _null_;         input place $ 1-40;         name=propcase(place);         put name;         datalines;      INTRODUCTION TO THE SCIENCE OF ASTRONOMY      VIRGIN ISLANDS (U.S.)      SAINT KITTS/NEVIS      WINSTON-SALEM, N.C.      ;            run;            SAS writes the following output to the log:             Introduction To The Science Of Astronomy      Virgin Islands (U.S.)      Saint Kitts/Nevis      Winston-Salem, N.C. |
| rank（x）                                                    | 返回一个字符在ascii或者edcdic码中的位置                      |                                                              |
| RIGHT(argument)                                              | 将字符右对齐                                                 | a='Due Date  ';      b=right(a);      put a $10.;      put b $10.; |
| VERIFY(source,excerpt-1<,...excerpt-n>)                      | 返回STRING中第一个不为X字符的位置                            | data scores;         input Grade : $1. @@;         check='abcdf';         if verify(grade,check)>0 then               put @1 'INVALID ' grade=;         datalines;      a b c b c d f a a q a b d d b      ;      结果是：INVALID Grade=q |
| REVERSE(X)                                                   | 将字符串X颠倒过来                                            |                                                              |







## 所有的

| 1.字符函数                                                   |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Anyalnum(参数，n)                                            | *从n开始计算出现第一个字符或者数字的位置是多少*/             |
| ANYALPHA(arg,start)：                                        | 返回第一次出现任意字母的位置，可选开始位置start。            |
| ANYDIGIT(arg,start)：                                        | 返回第一次出现任意数字的位置，可选开始位置start。            |
| ANYSPACE(arg,start)：                                        | 返回第一次出现任意空白的位置，可选开始位置start。            |
| BYTE(n)                                                      | 返回ASCII码值为n所对应的字符                                 |
| COLLATE(X,Y)                                                 | 返回ASCII码起始位置为X，终止位置为Y之间所有的字符            |
| Cat(arg1,arg2,....argn)                                      | 连接字符串并且保留原来字符串之间的空格                       |
| Cats(agr1,arg2,...,argn)                                     | 连接字符串并且去掉原来字符之间的空格                         |
| Catx('separator-sign',arg1,arg2,...,argn)                    | 连接字符串去掉字符串间的空格增加设定的连接符                 |
| CHAR(string,   position)                                     |                                                              |
| COALESCEC Function                                           |                                                              |
| COMPRESS(<source><,   chars><, modifiers>)                   | 压缩字符串移除字符串中指定的符号默认移除空格                 |
| COMPBL(X)                                                    | 把字符串X中多余空格去掉，即将连续多个空格压缩为一个          |
| COUNT(string,substring<,modifiers>)                          |                                                              |
| COUNTC(string,characters<,modifiers>)                        |                                                              |
| COUNTW(<string><, chars><, modifiers>)                       |                                                              |
| dequote                                                      |                                                              |
| FIND(string,substring<,modifiers><,startpos>)                |                                                              |
| FINDC(string,characters<,modifiers><,startpos>)              |                                                              |
| FIRST(string)                                                |                                                              |
| IFC(logical-expression,   value-returned-when-true, value-returned-when-false   <,value-returned-when-missing>) |                                                              |
| IFN(logical-expression,   value-returned-when-true, value-returned-when-false   <,value-returned-when-missing>) |                                                              |
| KSCAN(argument,n<,   delimiters>)                            |                                                              |
| length(str)                                                  | 返回指定字符串的长度 字符串尾部的空格不计算在内              |
| Substr(str,n,m)                                              | 从位置n开始从字符串中提取m个字符                             |
| Translate(string,to,from,<,...to-n,from-n>)                  | 变换字符串中字符的顺序，或者替换字符。                       |
| Tranwrd(str,’from’,’to’)                                     | 将字符串中的某些字符替换为其他字符。                         |
| PROPCASE(arg)                                                | 首字母大写。                                                 |
| TRIM(arg)：                                                  | 删除尾部空白。                                               |
| UPCASE(arg)：                                                | 替换成大写。                                                 |
| REPEAT(s,n)                                                  | 字符表达式s重复n次。                                         |
| INPUT(source, <?   \| ??>informat.)                          | input函数可以将字符型变量转换为字符型或数值型，这取决于指定的输入格式informat；而inputn函数只能将字符型变量转换为数值型。从这个角度上看，跟inputc函数一样，可以将inputn函数的功能理解为input函数功能的子集。 |
| PUT(source,   format.)                                       | 数值型转换成字符型                                           |
| SCAN(string ,n<, delimiter(s)>)                              | char是分隔符，i是取第几部分                                  |
| NLITERAL(string)                                             | 将字符转为化sas格式                                          |
| NOTDIGIT(string <,start>)                                    | 返回字符串中第一个不是数字的字符的位置，起始位置可选         |
| NOTLOWER(string <,start>)                                    | 返回字符串中第一个不是小写字符的位置，起始位置可选           |
| propcase(argument <,delimiter(s)>)                           | 将所有的字母转化为适当的形式，也就是都是小写，除了空格和/等分隔符之后的第一个字母大写，也可以自定义分隔符 |
| rank（x）                                                    | 返回一个字符在ascii或者edcdic码中的位置                      |
| RIGHT(argument)                                              | 将字符右对齐                                                 |
| VERIFY(source,excerpt-1<,...excerpt-n>)                      | 返回STRING中第一个不为X字符的位置                            |
| REVERSE(X)                                                   | 将字符串X颠倒过来                                            |
|                                                              |                                                              |
| 2.算术函数：                                                 |                                                              |
| ABS(X)                                                       | 求x的绝对值                                                  |
| DIM<n>(X)                                                    | 求数组中的元素个数，X为数组名，n为该数组的维数               |
| DIM(X, n)                                                    | 求多维数组的某一维中的元素个数，X为数组名，n为指定的维数     |
| HBOUND<n>(X)                                                 | 求数组的上界                                                 |
| HBOUND（X，n）                                               | 求多维数组中的某一维的上界，X为数组名，n为指定的维数         |
| LBOUND<n>(X)                                                 | 求数组的下界                                                 |
| LBOUND（X，n）                                               | 求多维数组中的某一维的下界，X为数组名，n为指定的维数         |
| MAX(X,Y,Z)                                                   | 求一串数中最大的一个，例如MAX(1,2,3,4)=4                     |
| MIX(X,Y,Z)                                                   | 求一串数中最小的一个，例如MAX(1,2,3,4)=1                     |
| MOD(X,Y)                                                     | 求X除以Y的余数，例如MOD(9,5)=4                               |
| SIGN(X)                                                      | 计算X的符号，结果为1,、-1或0                                 |
| SQRT(X)                                                      | 求X的平方根                                                  |
|                                                              |                                                              |
| 3.       数学函数                                            |                                                              |
| AIRY(x)                                                      | 计算AIRY函数的值                                             |
| EXP(x)                                                       | 指数函数 。                                                  |
| ERF(x)                                                       | 误差函数                                                     |
| GAMMA(x)                                                     | 完全函数                                                     |
| DAIR(x)                                                      | 计算DAIR函数的衍生值                                         |
| DIGAMMA(argument)                                            | 计算DIGAMMA函数的值                                          |
| ERF(argument)                                                | 计算偏差函数的值                                             |
| EXP(argument)                                                | 指数函数                                                     |
| GAMMA(argument)                                              | 计算伽马函数的值                                             |
| IBESSEL(nu, x, kode)                                         | 计算修正的bessel函数值                                       |
| JBESSEL(nu, x)                                               | 计算bessel函数值                                             |
| LGAMMA(argument)                                             | 计算伽马函数值的对数                                         |
| LOG(argument)                                                | 自然对数函数                                                 |
| LOG2(argument)                                               | 以2为底的对数函数                                            |
| LOG10(argument)                                              | 以10为底的对数函数                                           |
| ROUND(x,eps)                                                 | 求x按照eps指定的精度四舍五入后的结果，比如ROUND(5654.5654,0.01)   结果为5654.57，ROUND(5654.5654,10)结果为5650 |
| TRIGAMMA(argument)                                           | 计算三元的伽马函数值                                         |
|                                                              |                                                              |
| 4． 概率与密度函数                                           |                                                              |
| CDF(‘dist’, quantile,   parm-1,…, parm-k)                    | 计算累计分布函数，dist为分布名称，随后指定相关参数           |
| LOGPDF(‘dist’, quantile,   parm-1,…, parm-k)                 | 计算概率密度函数的对数                                       |
| LOGSDF(‘dist’, quantile,   parm-1,…, parm-k)                 | 计算生存函数的对数值                                         |
| PDF\|PMF(‘dist’, quantile,   parm-1,…, parm-k)               | 计算概率密度函数                                             |
| POISSON(m, n)                                                | 计算服从均数为m的POISSON分布变量值小于n的概率值              |
| PROBBETA(x, a, b)                                            | 计算BETA分布的概率值                                         |
| PROBBNML(p, n,m)                                             | 计算总体概率为P的二项分布在n次试验中成功次数小于等于m次的概率 |
| PROBCHI(x, df<, nc>)                                         | 计算卡方分布的概率值                                         |
| PROBF(x, ndf, ddf<,   nc>)                                   | 计算F分布的概率值                                            |
| PROBGAM(x, a)                                                | 计算伽马分布的概率值                                         |
| PROBHYPR(N, K, n, x, r>)                                     | 计算超几何分布的概率值                                       |
| PROBNEGB(p, n, m)                                            | 计算负二项分布的概率值                                       |
| PROBBNRM(x, y, r)                                            | 标准的二元正态函数                                           |
| PROBNORM(x)                                                  | 标准的正态分布函数值                                         |
| PROBT(x, df<, nc>)                                           | 计算t分布的概率值                                            |
| SDF(‘dist’, quantile,   parm-1,…, parm-k)                    | 计算生存函数                                                 |
|                                                              |                                                              |
| 5． 分位数函数                                               |                                                              |
| BETAINV(p, a, b)                                             | 计算分布参数为a、b的beta分布的第p百分位数                    |
| CINV(p, df<, nc>)                                            | 计算卡方分布的分位数                                         |
| FINV(p, ndf, ddf<, nc>)                                      | 计算F分布的分位数                                            |
| GAMINV(p, a)                                                 | 计算伽马分布的分位数                                         |
| PROBIT(p)                                                    | 计算标准正态分布的分位数                                     |
| TINV(p, df<, nc>)                                            | 计算t分布的分位数                                            |
|                                                              |                                                              |
| 6． 随机函数                                                 |                                                              |
| NORMAL(seed)                                                 | 计算服从正态分布的随机函数                                   |
| RANBIN(seed, n, p)                                           | 计算服从二项式分布的随机函数                                 |
| RANCAU(seed)                                                 | 计算服从柯西分布的随机函数                                   |
| RAND(‘dist’, parm-1,…, parm-k)                               | 根据特定的分布产生随机数（尚在测试阶段）                     |
| RANEXP(seed)                                                 | 产生服从指数分布的随机数                                     |
| RANGAM(seed, a)                                              | 产生服从伽马分布的随机数                                     |
| RANNOR(seed)                                                 | 产生服从正态分布的随机数                                     |
| RANPOI(seed, m)                                              | 产生服从Poisson分布的随机数                                  |
| RANTBL(seed, p1,..pi..pn)                                    | 由列表的概率分布产生随机数                                   |
| RANTRI(seed, h)                                              | 产生服从三角分布的随机数                                     |
| RANUNI(seed)                                                 | 产生服从均匀分布的随机数                                     |
| UNIFORM(seed)                                                | 产生服从均匀分布的随机数                                     |
|                                                              |                                                              |
| 7． 样本统计函数                                             |                                                              |
| CSS(argument, argument, …)                                   | 计算指定数值列表的离差平方和                                 |
| CV(argument, argument, …)                                    | 计算变异系数                                                 |
| KURTOSIS(argument, argument,   …)                            | 计算峰度系数                                                 |
| MAX(argument, argument, …)                                   | 计算最大值                                                   |
| MIN(argument, argument, …)                                   | 计算最小值                                                   |
| MEAN(argument, argument, …)                                  | 计算均值                                                     |
| MISSING(num exp \| character   expression)                   | 检验数据是否含有缺失值                                       |
| N(argument, argument, …)                                     | 计算样本个数，不包括缺失值                                   |
| NMISS(argument, argument, …)                                 | 计算样本中缺失值个数                                         |
| ORDINAL(count, argument,   argument, …)                      | 计算列表中第count个数值                                      |
| RANGE(argument, argument, …)                                 | 计算全距最大值与最小值的差                                   |
| SKEWNESS(argument, argument,   …)                            | 计算偏度系数                                                 |
| STD(argument, argument, …)                                   | 计算标准差                                                   |
| STDERR(argument, argument, …)                                | 计算标准误                                                   |
| SUM(argument, argument, …)                                   | 计算总和                                                     |
| USS(argument, argument, …)                                   | 计算平方和                                                   |
| VAR(argument, argument, …)                                   | 计算方差                                                     |
|                                                              |                                                              |
| 8． 三角函数                                                 |                                                              |
| ARCOS(argument)                                              | 反余弦函数                                                   |
| ARSIN(argument)                                              | 反正弦函数                                                   |
| ATAN(argument)                                               | 反正切函数                                                   |
| COS(argument)                                                | 余弦函数                                                     |
| COSH(argument)                                               | 双曲余弦函数                                                 |
| SIN(argument)                                                | 正弦函数                                                     |
| SINH(argument)                                               | 双曲正弦函数                                                 |
| TAN(argument)                                                | 正切函数                                                     |
| TANH(argument)                                               | 双曲正弦函数                                                 |
|                                                              |                                                              |
| 9． 截断函数                                                 |                                                              |
| CEIL(argument)                                               | 如果当前数值和整数部分的差距在10-12以内，则直接取整数，否则取大于原值的最小整数 |
| ceilz（argument）                                            | 取大于原值的最小整数，不fuzz                                 |
| FLOOR(argument)                                              | 计算小于或等于自变量的最大的整数                             |
| FUZZ(argument)                                               | 如果当前数值和整数部分的差距在10-12以内则直接取整数          |
| INT(argument)                                                | 计算自变量的整数部分                                         |
| ROUND(argument, unit)                                        | 按unit给定的数量单位进行四舍五入                             |
| TRUNC(argument, length)                                      | 将数据截为特定的长度                                         |
|                                                              |                                                              |
| 10． 日期时间函数                                            |                                                              |
| DATDIF(sdate, edate, basis)                                  | 计算两个日期之间相距的天数，basis指定SAS中的时间格式         |
| DATE()                                                       | 计算当月的日期作为SAS日期数据                                |
| DATEJUL(julian-date)                                         | 将Julian日期格式转换为SAS日期格式                            |
| DATEPART(datetime)                                           | 从日期时间格式的数据中抽取日期                               |
| DATETIME()                                                   | 计算当前日期时间值                                           |
| DAY(date)                                                    | 从SAS日期值得出是几号                                        |
| DHMS(date, hour, minute,   second)                           | 从日期小时分钟秒四个数值得到SAS日期时间值                    |
| HMS(hour, minute, second)                                    | 从小事分钟秒三个值计算一个SAS日期时间值                      |
| HOUR(<time \|datetime>)                                      | 从SAS时间或SAS日期时间中计算小时的数值                       |
| INTCK(‘interval’, from, to)                                  | 计算给定时间段中的间隔的个数                                 |
| INTNX(‘interval’, start-from,   increment<, ‘alignment’>)    | 计算在一定时间后的SAS日期时间值                              |
| INTCYCLE(interval   <<multiple.<shift-index>>>)              | 返回高一级的日期周期                                         |
| INTSEAS(interval<<multiple.<shift-index>>>)                  | 返回高一级的周期中包含的本周期的数值                         |
| INTTEST(interval<<multiple.<shift-index>>>)                  | 测试一个间隔形式是否有效                                     |
| JULDATE(date)                                                | 将SAS日期格式转换为Julian日期                                |
| MDY(month,day,year)                                          | 从月日年得到一个SAS日期值                                    |
| MINUTE(time \|datetime)                                      | 从时间值或日期时间值中抽取分钟值                             |
| MONTH(date)                                                  | 从日期中得到月份                                             |
| QTR(date)从SAS                                               | 日期值得到对应的季度                                         |
| SECOND(time \| datetime)                                     | 从SAS时间值或SAS日期时间值中得到秒                           |
| TIME                                                         | 计算当前时间                                                 |
| TIMEPART                                                     | 从日期时间值中抽取时间值                                     |
| TODAY                                                        | 计算当前日期                                                 |
| WEEKDAY                                                      | 从SAS日期值得到为星期几                                      |
| YEAR                                                         | 由SAS日期值得到年份                                          |
| YRDIF(sdate,edate,basis)                                     | 计算两个日期之间所差的年份                                   |
| YYQ                                                          | 从年份和季度产生一个SAS日期值                                |
|                                                              |                                                              |


## 12hanshu

| 12.keywords                                                  |                                                    |
| ------------------------------------------------------------ | -------------------------------------------------- |
| merge                                                        | 将几个数据集中的观察值链接成一个数据集             |
| update                                                       | 用交易数据批量更新原始主表中的数据                 |
| modify                                                       | 用交易数据更新原始主表的数据                       |
| set                                                          | 从一个或者多个数据集中读取观察值                   |
| keep                                                         | 确定set中哪些变量要保留                            |
| drop                                                         | 确定set中哪些变量要删除                            |
| key                                                          | 用于set的lookup，指定要查找的变量列                |
| by                                                           | 配合update modify和merge控制排序或者建立特殊的分组 |
| subsetting IF statement                                      | 中止当前循环读取的数据，不讲读取的数据输入到data   |
| RENAME=                                                      | 改变变量的名字                                     |
| stop                                                         | 停止当前data步骤，进入data后的程序                 |
| IF-THEN/ELSE Statement                                       | 根据条件执行语句                                   |
| DO index-variable = start TO stop BY   increment;              action statements;         END; | 将一个语句执行多遍                                 |
| input statement                                              | 描述数据记录中的结构，并赋值给相应的sas变量        |



## 参考文献

