# calendar
The difference between the Gregorian calendar and the Julian calendar.

>MySQL uses what is known as a proleptic Gregorian calendar.
>
>Every country that has switched from the Julian to the Gregorian calendar has had to discard at least ten days during the switch. To see how this works, consider the month of October 1582, when the first Julian-to-Gregorian switch occurred.

|Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday|
|-|-|-|-|-|-|-|
|1|2|3|4|15|16|17|
|18|19|20|21|22|23|24|
|25|26|27|28|29|30|31|
>
>There are no dates between October 4 and October 15. This discontinuity is called the cutover. Any dates before the cutover are Julian, and any dates following the cutover are Gregorian. Dates during a cutover are nonexistent.
>
>A calendar applied to dates when it was not actually in use is called proleptic. Thus, if we assume there was never a cutover and Gregorian rules always rule, we have a proleptic Gregorian calendar. This is what is used by MySQL, as is required by standard SQL. For this reason, dates prior to the cutover stored as MySQL `DATE` or `DATETIME` values must be adjusted to compensate for the difference. It is important to realize that the cutover did not occur at the same time in all countries, and that the later it happened, the more days were lost. For example, in Great Britain, it took place in 1752, when Wednesday September 2 was followed by Thursday September 14. Russia remained on the Julian calendar until 1918, losing 13 days in the process, and what is popularly referred to as its “October Revolution” occurred in November according to the Gregorian calendar. 
>
>来自[MySQL官方文档12.8 What Calendar Is Used By MySQL?](https://dev.mysql.com/doc/refman/5.7/en/mysql-calendar.html)
