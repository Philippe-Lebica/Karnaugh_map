# Karnaugh_map

Code for beginner: two digits decimal rule

In memory of Maurice Karnaugh, RIP!

The purpose of this tutorial is to hide useless zero from the decimal part of a number. In this real case study, I need the code for Crystal Report (Basic). The most important here is the logical process to generate the code, do not start #coding right away!

1) INPUT and OUTPUT
Sample data:
INPUT => Display => OUTPUT 
1.22 => 1.22 => 2 
2.30 => 2.3 => 1 
3.04 => 3.04 => 2 
4.00 => 4 => 0 
 
INPUT is any number showing two decimals, even with zeros.
OUTPUT is the number of digits to be displayed (0, 1 or 2)

This was a test for an #intern in my last job, let's make the code.
My solution in the first comment.
You may find a tip somewhere on this page...

Here my solution :
2) Logical process analysis 
I use the Karnaugh map to define if the first and/or second decimal is equal to zero. Just full filled the table with all possible combinations (2^n solutions) and then analyse the result.
Variables:  *.D1D2
D1 first decimal digit, D2 second decimal digit
Is D1 or D2 equal to zero? 1 for yes, 0 for no.
D1	D2		OUTPUT	Note
0	  0		  2	      No zero: show all digits
0	  1		  1	      The right digit is equal to zero: show only one digit
1	  0		  2	      The right digit is not equal to zero: show all digits
1	  1		  0	      All are equal to zero: show no digit

3) Code, at last!
I can group the OUTPUT = 2 only depending on D2 value.
if D2 = 0 then OUTPUT = 2 

And then test D1 in the else clause
if D2 = 0 then OUTPUT = 2
	else (if D1 = 0 then OUTPUT = 1
		else OUTPUT = 0)
Crystal Report real code I used in production, replace {MyNumber} by your own variable and copy the code into the Format/Decimal formula of your number:
stringVar D1 := left(ToText(remainder({MyNumber},1)),1); 
stringVar D2 := right(ToText(remainder({MyNumber},1)),1); 
if D2 = "0" then 2
else (if D1 = "0" then 1 
else 0)

