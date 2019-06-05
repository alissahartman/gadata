TO_CHAR													

The TO_CHAR function converts data from various data types to character data. 	

There are three versions of TO_CHAR: 

	TO_CHAR(Character)			
	TO_CHAR(Number)
	TO_CHAR(Date)	

The following sections describe each of the three TO_CHAR functions.									
													
TO_CHAR(CHARACTER)
--------------------
Syntax: TO_CHAR(c)													
Parameters: c is either an NCHAR, an NVARCHAR2, a CLOB, or an NCLOB.									Process: Transforms the incoming parameter into a VARCHAR2.										Output: VARCHAR2.													
Example:													
	
	SELECT TO_CHAR('Hello') AS NEW FROM DUAL;

|NEW  |
|:---:|
|Hello|

For the TO_CHAR it may not seem like muched happened because most of this is behind the scenes. Remember we have a field that is 
NCHAR,NVARCHAR2,CLOB, or NCLOB. Using TO_CHAR we are converting the data type to VARCHAR which will help reduced unused space and VARCHAR leans itself to being more friendly to other functions. 
																			
									
													
TO_CHAR(NUMBER)
------------------
Syntax: TO_CHAR(n, format_model, nls_parms)												
Parameters: n is a number (required). The parameter format_model is optional. 
A format model consists of one or more format elements,
The nls_parms value is the same parameter you saw earlier with the TO_NUMBER function.													
Process: Transforms n into a character string, using the optional format model for guidance as to how to format the output with any special characters that may be desired, such as dollar signs or other financial symbols, special handling of negative numbers.
Output: Character.													

Example: Format the number 198 with a dollar sign and penny specification.													
													
	SELECT TO_CHAR(198,'$999.99') FROM DUAL;		
													
|TO_CHAR(198,'$999.99')|													
|:--------------------:|
|$198.00|													




TO_CHAR(DATE)
--------------------------
Syntax: TO_CHAR(d, format_model, nls_parms)	
Parameters: d is a date or a date interval (required). 
The parameter format_model is optional and can be used to format data in a variety of ways. 
The nls_parms parameter is the same as you saw earlier for the TO_NUMBER function.													
|Element|Description|
|:-----:|:---------:|
|AD/A.D.|-|
|BC/B.C.|Anno Domini or Before Christ indicator, with or without periods.|							
|AM/A.M.|													
|PM/P.M.|Morning or afternoon hours, with or without periods.|
|CC/SCC|Century.|												
|D|Day of the week, 1 through 7.|												
|DAY|The name of the day spelled out.|												
|DD|Day of the month, 1 through 31.|												
|DDD|Day of the year, 1 through 366.|												
|DL|Long date format, as determined by the NLS_DATE_FORMAT parameter.| 
The appearance is determined by the NLS_TERRITORY and NLS_LANGUAGE parameters. Sample AMERICAN_AMERICA output is "Saturday, July 27, 2019."												
|DS|Short date format. Appearance is determined by the NLS_TERRITORY and NLS_LANGUAGE parameters.| 
Sample AMERICAN_AMERICA output is "7/27/2019."												
|DY|Abbreviated name of day, such as SUN, MON, TUE, and so on.|												
E	Abbreviated era name.												
EE	Full era name.												
FF	Fractional seconds.												
FM	Used in combination with other elements to direct the suppression of leading or trailing blanks.												
FX	Exact matching between the character data and the format model.												
HH, HH12	Hour of the day, 1 through 12 (both are identical). 12 midnight is represented as 12.												
HH24	Hour of the day, 1 through 24. 12 midnight is represented by 00.												
IW	Week of the year, 1 through 53.												
I													
IY													
IYY	Last one, two, or three digits of the ISO year.												
J	Julian day, counted as the number of days since January 1, 4712 B.C.												
MI	Minute. 0 through 59.												
MM	Month in double digits, 01 through 12.												
MON	Abbreviated name of month, such as JAN, FEB, MAR.												
MONTH	Name of month spelled out.												
PR	If negative, numbers are enclosed within angle brackets (<>). If positive, returned with leading and trailing spaces. PR follows specification, for example: 9999PR.												
Q	Quarter of year.												
RM	Roman numeral month.												
RR	Accepts twentieth-century dates in the twenty-first century using only two digits. 00 through 49 is interpreted as 2000 through 2049. 50 through 99 is interpreted as 1950 through 1999.												
RRRR	The four-digit year. If provided a two-digit year, it returns the same value as RR.												
SS	Seconds, 0 through 59.												
SSSS	Seconds past midnight, 0 through 86399.												
TS	The short time format. Allowable only when specified with the DL or DS format model element, separated by white space.												
TZD	Abbreviated time zone with daylight saving time. Valid only in timestamp and interval formats. Examples: EST, CMT.												
TZH	Time zone hour. Not valid in DATE data types; valid only in timestamp and interval formats. 00 through 12.												
TZM	Time zone minute. Valid only in timestamp and interval formats. 00 through 59.												
TZR	Time zone region information. Not valid in DATE data types; valid only in timestamp and interval formats. Example: America/Los_Angeles.												
WW	The week of the year, 1 through 53. Week 1 starts on the first day of the year and ends on the seventh day of the year.												
W	The week of the month, 1 through 5. Week 1 starts on the first day of the month and ends on the seventh day of the month.												
X	Local radix character. This is the character used in a numeric representation to separate an integer from its fractional part. In base 10 notation, the radix character is a decimal point, as in 17.2, where the decimal point separates the integer 17 from its fractional part of 0.2.												
Y,YYY	The year with the comma in position.												
YEAR, SYEAR	The year spelled out in English. The S version causes BC dates to display with a minus sign prefix.												
YYYY, SYYYY	The four-digit year. The S version causes BC dates to display with a minus sign prefix.												
YYY, YY, Y	The last three digits, two digits, or one digit of the year.												
- / , . ; :	Punctuation that is accepted in place and passed through as is.												
text	Literal value. Display as is.												
Table 6-3: Date Format Elements													
													
Output: Character.													
Example: Here’s an example of the use of a date format model, as described in Table 6-3:													
													
SELECT TO_CHAR(SYSDATE,'DAY, "THE" DD "OF" MONTH, RRRR')													
FROM DUAL;													
													
TO_CHAR(SYSDATE,'DAY,"THE"DD"OF"MONTH,RRRR')													
--------------------------------------------													
WEDNESDAY , THE 17 OF FEBRUARY , 2016													
The FM code is a format mask that cleans up all of the trailing blanks, as follows:													
													
SELECT TO_CHAR(SYSDATE,'FMDAY, "THE" DD "OF" MONTH, RRRR') FROM DUAL;													
													
TO_CHAR(SYSDATE,'FMDAY,"THE"DD"OF"MONTH,RRRR')													
----------------------------------------------													
WEDNESDAY, THE 17 OF FEBRUARY, 2016													
Changing the format masks to mixed case sends an implied message to mix-case the output as well.													
													
SELECT TO_CHAR(SYSDATE,'FMDay, "the" Dd "of" Month, RRRR')													
FROM DUAL;													
													
TO_CHAR(SYSDATE,'FMDAY,"THE"DD"OF"MONTH,RRRR')													
													
----------------------------------------------													
Wednesday, the 17 of February, 2016													
Adding the th indicator introduces an additional improvement. The inclusion of th will append whatever is appropriate after the date—for 1, you’ll get “1st”; for 2, you’ll get “2nd”; and so on. Here’s an example:													
													
SELECT TO_CHAR(SYSDATE,'FMDay, "the" Ddth "of" Month, RRRR')													
FROM DUAL;													
													
TO_CHAR(SYSDATE,'FMDAY,"THE"DDTH"OF"MONTH,RRRR')													
------------------------------------------------													
Wednesday, the 17th of February, 2016													
The format model is the secret to extracting the time values from SYSDATE. Here’s an example:													
													
SELECT TO_CHAR(SYSDATE,'HH24:MI:SS AM') FROM DUAL;													
													
TO_CHAR(SYSDATE,'HH24:MI:SSAM')													
												
17:48:16 PM													
Notice in this example we can use either AM or PM to indicate where we want the morning/afternoon indicator to be located and whether we want it to include periods. Whether we use AM or PM makes no difference; the appropriate indicator will appear wherever the format model directs, as shown in the preceding example.													
													
The SYSDATE function displays the current date by default as stored on the server on which the database is installed. But buried inside of it is also the time of day, in hours, minutes, and seconds. The full set of data can be extracted from SYSDATE with the format model parameters of the TO_CHAR function, as shown in Table 6-3. But beware, there is danger here, and it’s yet another example of how tricky SQL can be. Take a look at this SQL statement:													
													
SELECT TO_CHAR(SYSDATE, 'DD-MON-RRRR HH:MM:SS') "Today's Date And Time"													
FROM DUAL;													
See anything wrong with it? Perhaps not. Most developers don’t; this can trip up even the most experienced and seasoned of SQL professionals. Try it on any database instance, and it will work, and the output will probably appear to be correct. But look closely at the value displayed for that portion of the format model represented by MM. Then look at Table 6-3. MM is not minutes; it is months. If you want minutes, you need to use MI, as in HH:MI:SS. Watch this one, folks; it’s tricky—the syntax is technically correct, the execution will be successful, and the test data looks correct at a glance. But it’s still wrong. The sharp eye of a certified Oracle Database SQL Expert should flag this.													
													
The YY and RR format masks interpret two-digit year representations differently. See the following query:													
													
SELECT TO_CHAR(TO_DATE('01-JAN-49','DD-MON-YY'),'YYYY'),													
TO_CHAR(TO_DATE('01-JAN-50','DD-MON-YY'),'YYYY'),													
TO_CHAR(TO_DATE('01-JAN-49','DD-MON-RR'),'RRRR'),													
TO_CHAR(TO_DATE('01-JAN-50','DD-MON-RR'),'RRRR')													
FROM DUAL;													
													
TO_C TO_C TO_C TO_C													
---- ---- ---- ----													
2049 2050 2049 1950													
Note that a date entered as 50 is interpreted as 2050 by the YYYY format mask, but 1950 is entered as RRRR. See Table 6-3 for more information about YYYY and RRRR.													
													
The hour of midnight is the starting moment of a new day. The value for midnight is stored consistently but represented differently based on the format model used. In a 24-hour format (HH24), midnight is represented as 00, but in a 12-hour format (HH12 or HH) midnight is represented as 12. For example, we can specify a date literal at 12 midnight as a string, convert it to a DATE data type using TO_DATE, and then use TO_CHAR with a format mask to illustrate the point.													
													
SELECT TO_CHAR(TO_DATE('07-JUL-16 00:00:00','DD-MON-YY HH24:MI:SS'),													
DD-MON-YY HH24:MI:SS PM') AS MIDNIGHT_HR24,													
TO_CHAR(TO_DATE('07-JUL-16 00:00:00','DD-MON-YY HH24:MI:SS'),													
DD-MON-YY HH12:MI:SS PM') AS MIDNIGHT_HR12													
FROM DUAL;													
													
MIDNIGHT_HR24 MIDNIGHT_HR12													
--------------------- ---------------------													
07-JUL-16 00:00:00 AM 07-JUL-16 12:00:00 AM													
The first column takes the date literal '07-JUL-16' at midnight, converts it to a DATE data type in 24-hour format, and then converts it back to 24-hour format.													
													
The second column starts with the same DATE value but uses TO_CHAR to display the date value with a 12-hour format. Remember that the PM format model specifies the display of PM or AM, whichever is appropriate.													
													
The 24-hour format shows midnight as 00, and the 12-hour format shows midnight as 12. The value stored is not different. Only the representation is different, in accordance with the format model specified.													
													
