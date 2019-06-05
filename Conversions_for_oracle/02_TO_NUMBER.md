TO_NUMBER						
	Syntax: TO_NUMBER(e1, format_model, nls_parms)					
	Parameters: e1 is an expression (required); format_model is the optional format model. See Table 6-1 for a complete list of elements that make up the format model.					
	ransform e1 from an expression, perhaps a character string, into a numeric value, using format_model to determine what format e1 may take and where to extract the numeric values from among the formatting information.					
	Output: Numeric.					
Example: In the example that follows, our starting value is a string, '$17,000.23'. This isn’t a numeric data type but a character string containing a dollar sign and a comma. The format model here explains that the dollar sign is a symbol and makes it clear where the significant numeric data can be found in the source column. The 9 element in the following example is not a literal number 9 but rather an element of the format model that indicates the presence of any digit. It is repeated to indicate the upper bound of acceptable values. Finally, the output is displayed—a raw numeric value extracted from the character string '$17,000.23'.						
	SELECT TO_NUMBER('$17,000.23','$999,999.99')					
	FROM DUAL;					
	TO_NUMBER('$17,000.23','$999,999.99')					
	17000.23					
						
Here is a similar example showing the use of the nls_parms parameter:						
	SELECT TO_NUMBER('17.000,23',					
	999G999D99',					
	nls_numeric_characters='',.'' ')					
	REFORMATTED_NUMBER					
	FROM DUAL;					
	REFORMATTED_NUMBER					
	17000.23					
						
In this example, the incoming value shows a decimal point to mark “thousands” and the comma to mark the decimal point. The nls_parms value clarifies this to the TO_NUMBER function, along with the format mask, and the incoming value is interpreted and translated, as shown in the displayed output.						
		
						
|Element|Example|Description|
|:------|:------|:----------|
|, .|9,999.99|Commas and decimal points will pass through wherever they are included.|		
|$|$999.99|Leading dollar sign.|
|0|99.99|Leading or trailing 0.|			
|9|999|Any digit.|			
|B|B999|Leading blank for integers.|			
|C|C999|The ISO currency symbol as defined in the NLS_ISO_CURRENCY parameter.|			
|D|999D99|Returns the current decimal character as defined by the NLS_NUMERIC_CHARACTERS parameter. The default value is a period.|	|EEEE|9.9EEE|Returns a value in scientific notation.|			
|G|9G999|Returns the group separator (e.g., a comma).|			
|L|L999|Returns the local currency symbol.|			
|MI|999MI|Returns negative value with trailing minus sign; returns positive value with a trailing blank.|			
|PR|999PR|Returns negative values in angle brackets.|			
	RN					
	rn	RN	Returns values in Roman numerals, uppercase. Put RN in lowercase (as in "rn") for Roman numerals in lowercase.			
	S (prefix)	S9999	Returns negative values with a leading minus sign, positive values with a leading positive sign.			
	Note: Can appear only in the first or last position of a format mask.					
	S (suffix)	9999S	Returns negative values with a trailing minus sign, positive values with a trailing positive sign.			
	Note: Can appear only in the first or last position of a format mask.					
	TM	TM	The text minimum number format model returns the smallest number of characters possible.			
	U	U999	Returns the Euro currency symbol or whatever is indicated by the NLS_DUAL_CURRENCY parameter.			
	V	999V99	Returns a value multiplied by 10n, where n is the number of 9s after the V.			
	X	XXXX	Returns the hexadecimal value.			
						
	Warning: Only one period is allowed per format mask.					
	There is an optional third parameter representing NLS settings. It allows you to identify any of the three NLS parameters defined in Table 6-2. If included, the third parameter for TO_NUMBER consists of a single string that encompasses any one or more of those three NLS parameters. For example, the following is one example of the nls_parms parameter that provides a specification of two of the NLS parameters:					
						
	NLS Parameter	Description				
	NLS_NUMERIC_CHARACTERS = 'dg'	d = decimal character (see D in Table 6-1)				
	g = group separator (see G in Table 6-1)					
	NLS_CURRENCY = 'text'	text = local currency symbol (see L in Table 6-1)				
	NLS_ISO_CURRENCY = 'currency'	currency = international currency symbol (see C in Table 6-1)				
						
						
