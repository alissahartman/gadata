Conversion functions can do more than change a value’s data type. 
Some conversion functions also feature formatting capabilities. 
For example, if you have a DATE data type that contains raw information about hours, minutes, seconds, and the date on the calendar,
you can transform it into a text string that spells out the entire date in detail, 
such as “Thursday, July the Fourth, Seventeen Seventy-Six.”								
								
EXPLICIT VS IMPLICIT Conversion								
								
IMPLICIT								
Implicit occurs automatically in circumstances where SQL will determine on its own that a data type conversion is required but not specified. When this happens, SQL will perform the data type conversion automatically.								
	SELECT 'Chapter ' || 1 || ' ... I am born.'							
	FROM   DUAL;							
	CHAPTER'||1||'...IAMBORN.'							
	Chapter 1 ... I am born.							
	the second value in the SELECT list is numeric yet is included in a text function for performing string concatenation automatically converting it to a string							
								
	SELECT SYSDATE,							
	ADD_MONTHS(SYSDATE,							
	SUBSTR('plus 3 months',6,1)) PLUS_THREE							
	FROM   DUAL;							
	SYSDATE                   PLUS_THREE							
	17-FEB-16                 17-MAY-16							
The SUBSTR function in line 3 returns a string value of 3, which is automatically converted to a numeric data type 
since a numeric is what is required for the ADD_MONTHS function in lines 2 and 3.							
								
It is best practice and better programming to use Explicit conversions rather than rely on Implicit
(code is clear, documented and supportable)							
								
When comparing text and numeric values, such as in an IF statement, 
the text value will generally be converted to numeric. But not always:								
								
The following are some additional rules for automatic data type conversion:								
	Numeric values will generally not convert automatically to dates.							
	Numeric and text data will generally not convert automatically to very large sized types, such as LOB, CLOB, RAW, and others.							
	Very large types will generally not automatically convert to each other, such as from BLOB to CLOB, for example. 
  Some will, but many won’t.							
								
Implicit conversion can ignore indexes and thus slow down query performance								
								
EXPLICIT 								
	NUMERIC							
		TO_NUMBER						
	CHARACTER							
		TO_CHAR-Character						
		TO_CHAR-Number						
		TO_CHAR-Date						
								
	DATE							
		TO_DATE						
		TO_TIMESTAMP						
		TO_TIMESTAMP_TZ						
		TO_YMINTERVAL						
		TO_DSINTERVAL						
		NUMTOYMINTERVAL						
		NUMTODSINTERVAL						
	CAST							
