# The difference between the Gregorian calendar and the Julian calendar

本文主要讲公历和儒略历的区别。

[MySQL官方文档12.8 What Calendar Is Used By MySQL?](https://dev.mysql.com/doc/refman/5.7/en/mysql-calendar.html)里是这样说的：

> MySQL uses what is known as a proleptic Gregorian calendar.
>
> Every country that has switched from the Julian to the Gregorian calendar has had to discard at least ten days during the switch. To see how this works, consider the month of October 1582, when the first Julian-to-Gregorian switch occurred.

| Monday | Tuesday | Wednesday | Thursday | Friday | Saturday | Sunday |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | 2 | 3 | 4 | 15 | 16 | 17 |
| 18 | 19 | 20 | 21 | 22 | 23 | 24 |
| 25 | 26 | 27 | 28 | 29 | 30 | 31 |

> There are no dates between October 4 and October 15. This discontinuity is called the cutover. Any dates before the cutover are Julian, and any dates following the cutover are Gregorian. Dates during a cutover are nonexistent.
>
> A calendar applied to dates when it was not actually in use is called proleptic. Thus, if we assume there was never a cutover and Gregorian rules always rule, we have a proleptic Gregorian calendar. This is what is used by MySQL, as is required by standard SQL. For this reason, dates prior to the cutover stored as MySQL `DATE` or `DATETIME` values must be adjusted to compensate for the difference. It is important to realize that the cutover did not occur at the same time in all countries, and that the later it happened, the more days were lost. For example, in Great Britain, it took place in 1752, when Wednesday September 2 was followed by Thursday September 14. Russia remained on the Julian calendar until 1918, losing 13 days in the process, and what is popularly referred to as its “October Revolution” occurred in November according to the Gregorian calendar.

那么 `the Gregorian calendar` 和 `the Julian calendar` 分别是什么呢？

### 简介

**the Gregorian calendar**格里高利历，是公历的标准名称，是一种源自于西方社会的历法。它先由意大利医生、天文学家、哲学家、年代学家阿洛伊修斯·里利乌斯（Aloysius Lilius，约1519-1576）与克拉乌（Christophorus Clavius）等学者在儒略历的基础上加以改革，后由教皇格里高利十三世（Pope Gregory XIII）于1582年颁布。

**the Julian calendar**儒略历，是由罗马共和国独裁官儒略·恺撒（即盖乌斯·尤里乌斯·凯撒Gaius Julius Caesar）采纳数学家兼天文学家索西琴尼的计算后，于公元前45年1月1日起执行的取代旧罗马历法的一种历法。

### 公元来历

公元即“公历纪元”，又称“西元”。它以耶稣诞生之年作为纪年的开始。在儒略历与格里高利历中，在耶稣诞生之后的日期，称为主的年份Anno Domini（`A.D.`）（拉丁）。而在耶稣诞生之前，称为主前Before Christ（`B.C.`）。但是现代学者为了淡化其宗教色彩以及避免非基督徒的反感而多半改称用公元\(Common era，缩写为C.E.\)与公元前\(Before the Common Era，缩写为 B.C.E.\)的说法。

### 历史

* 在儒略历之前

  在儒略历发明之前，罗马人使用的是阴历，每个月29或30天，每两年插入一个闰月，闰月长度为3/4个普通月（也就是，第一年新月月初，第三年下弦月初，第五年满月月初，第七年上弦月初，第九年回到新月月初）。在这样一个历法系统里，常年355天、闰年377或378天，平均下来每年有366又1/4天。本来这个历法是为了切合太阳的运行规律的，但是由于闰月的添加是罗马神官们自行决定的，所以在战争时代或者其他一些宗教活动荒废的时候会有相当长的一段时间无法宣布一年为闰年，这样一来历法就会大大偏离太阳规律。同时由于消息传播的方式并不发达，远离城邦居住的居民甚至有时并不能了解到神官发布的闰年通告，经常会导致许多人对这天的日期一无所知。

  这个情况在凯撒当政时期变得颇为严重，因此凯撒决定进行历法改革，以永久的让历法和太阳运行规律结合起来，不受宗教活动或其他人为因素的影响。

* 儒略历内容

  **儒略历**以回归年为基本单位，是一部纯粹的阳历。它将全年分设为12个月，单数月是大月，长31日，双数月是小月，长为30日，只有2月平年是29日，闰年30日。每年设365日，每四年一闰，闰年366日，每年平均长度是365.25日。《儒略历》编制好后，儒略·恺撒的继承人奥古斯都又从2月减去一日加到8月上（8月的拉丁名即他的名字奥古斯都）使8月变成大月，又把9月、11月改为小月，10月、12月改为大月。

* 格里高利历内容

  **儒略历**比回归年365.2422日长0.0078日，400年要多出3.12日。从公元325年定春分为3月21日提早到了3月11日。1500年后由于误差较大，被罗马教皇格里高利十三世于1582年进行改善与修订，变为**格里高利历**，即沿用至今的世界通用的公历。**格里高利历**的主要内容就是改闰年方法为： 凡公元年数能被4整除的是闰年，但当公元年数后边是带两个“0”的“世纪年”时，必须能被400整除的年才是闰年。

### 问题

从儒略历到格里高利历，带来的问题就是需要处理因为之前的置闰方法多出来的天数。例如著名的**俄国十月革命**，它发生在公历1917年11月7日，但是是俄历也就是儒略历的1917年10月25日。这就是我们接下来要说的`Change From Julian to Gregorian Calendar`

### Change From Julian to Gregorian Calendar

在颁布**格里高利历**时，Pope Gregory XIII宣布1582年10月4日后的一天是10月15日，来清算公元325年以来积累的老账。

下面是一些国家在处理`Change From Julian to Gregorian Calendar`时的时间：

| Year of Switch | Country | Days Removed |
| --- | --- | --- |
| 1582 | France \(most areas\), Italy, Poland, Portugal, Spain | 10 days |
| 1583 | Austria, Germany \(Catholic states\), | 10 days |
| 1587 | Hungary, | 10 days |
| 1610 | Germany \(Prussia\), | 10 days |
| 1752 | United States \(most areas\), Canada \(most areas\),United Kingdom \(and colonies\) | 11 days |
| 1872/1873 | Japan, | 12 days |
| 1916 | Bulgaria, | 13 days |
| 1918 | Estonia, Russia, | 13 days |
| 1923 | Greece, | 13 days |
| 1926/1927 | Turkey, | 13 days |

来自[timeanddate.com](https://www.timeanddate.com/calendar/julian-gregorian-switch.html)

### 月份的命名：

> 古罗马历法，一年从March到February，前11个月以数字命名，最后一个月（February）是腊月。后来改历，January成为第一个月，各月名逐渐改用俗名或以神命名。  
> 1. 一月 **January** 名字来自古罗马神话的双面神雅努斯。  
> 2. 二月 **February** 名字来自古罗马的节日Februa。  
> 3. 三月 **March** 名字来自古罗马神话的战神玛尔斯。  
> 4. 四月 **April** 名字来自古罗马的词aperire，意思为“开始”，意味着春天开始。  
> 5. 五月 **May** 名字来自古罗马神话的花神玛亚。  
> 6. 六月 **June** 名字来自古罗马共和国的创始人Junius。  
> 7. 七月 原名Quintilis，后改**July**。古罗马历只有10个月，这是第五月，原名是“第五”的意思，因为恺撒是这月出生的，经元老院一致通过，将此月改为恺撒的名字“儒略”。  
> 8. 八月 原名Sextilis 后改**August**。原名是“第六”的意思，因为后来独裁者屋大维是生于此月，元老院将此月改为他的称号“奥古斯都”。  
> 9. 九月 **September** 拉丁语“第七”的意思。  
> 10. 十月 **October** 拉丁语“第八”的意思。  
> 11. 十一月 **November** 拉丁语“第九”的意思。  
> 12. 十二月 **December** 拉丁语“第十”的意思。

### 历史人物介绍：

> 盖乌斯·尤利乌斯·恺撒（Gaius Julius Caesar，公元前102年7月12日—公元前44年3月15日），史称恺撒大帝，罗马共和国（今地中海沿岸等地区）末期杰出的军事统帅、政治家，并且以其卓越的才能成为了罗马帝国的奠基者。  
> 恺撒出身贵族，历任财务官、祭司长、大法官、执政官、监察官、独裁官等职。  
> 公元前60年与庞培、克拉苏秘密结成前三头同盟，随后出任高卢总督，在8年的时间里征服了高卢全境（今法国一带），还袭击了日耳曼和不列颠。公元前49年，他率军占领罗马，打败庞培，集大权于一身，实行独裁统治。制定了《儒略历》。  
> 公元前44年3月15日，恺撒遭以布鲁图所领导的元老院成员暗杀身亡，享年58岁。恺撒死后，其甥孙及养子屋大维击败安东尼开创罗马帝国并成为第一位帝国皇帝。
>
> 盖乌斯·屋大维·奥古斯都（Gaius Octavius Augustus，公元前63年9月23日—公元14年8月19日），原名盖乌斯·屋大维·图里努斯（Gaius Octavian Thurinus），后三头同盟之一，罗马帝国的第一位元首（Princeps），元首政制的创始人，统治罗马长达40年，是世界历史上最为重要的人物之一。  
> 屋大维是恺撒的甥外孙，前44年被恺撒指定为第一继承人并收为养子。前43年，恺撒被刺后登上政治舞台，与安东尼、雷必达结成“后三头同盟”。前42年与安东尼在腓力比之战中打败共和派首领布鲁图和喀西。前36年，他剥夺雷必达的军权，后在阿克图海战打败安东尼，消灭了古埃及的托勒密王朝，回罗马后开始掌握一切国家大权。前30年，被确认为“终身保民官”，前29年获得“大元帅”（Imperator，又译“皇帝”）称号；前28年被元老院赐封为“奥古斯都”（意为神圣伟大）。并改组罗马政府，给罗马世界带来了两个世纪的和平与繁荣。  
> 屋大维曾先后获得执政官、保民官、大祭司长等职衔，实为罗马皇帝。为加强统治，对军队进行改革，实行雇佣兵制度；建立禁卫军，驻守罗马和意大利。对外继续扩张，向西完成对西班牙的征服，向北推进至多瑙河、莱茵河一线。他善于审时度势、进退有节，处事机智果断、谨慎稳健。他所采取的一系列顺乎形势的内外政策，开创了相对安定的政治局面，为帝国初期的繁荣打下基础。公元14年8月，在他去世后，罗马元老院决定将他列入“神”的行列。



