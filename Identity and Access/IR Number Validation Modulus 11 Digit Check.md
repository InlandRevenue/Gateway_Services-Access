![IRD logo](../Images/IRlogo.gif)<br/>
![Software Dev](../Images/SoftwareDev.png)

# IR Number Validation Modulus 11 Digit Check

The IRD number format used by Inland Revenue is an eight or nine digit number 
consisting of the following parts -
+ A seven or eight digit base number 
+ A trailing check digit 

## Check digit validation 

The following steps are to be performed -

#### 1. Check the valid range
* If the IRD number is < 10-000-000 or > 150-000-000 then the number is 
invalid. This step ensures that the IRD number is in the already issued 
range, or is in the range expected to be issued in the next 10 years.
#### 2. Form the eight digit base number: 
+ Remove the trailing check digit.
+ If the resulting number is seven digits long, pad to eight digits by adding a 
leading zero. 
#### 3. Calculate the check digit:
+ To each of the base number’s eight digits a weight factor is assigned. From 
left to right these are: `3, 2, 7, 6, 5, 4, 3, 2`. 
+ Sum together the products of the weight factors and their associated 
digits. 
+ Divide the sum by 11. If the remainder is 0 then the calculated check digit 
is 0.
+ If the remainder is not 0 then subtract the remainder from 11, giving the 
calculated check digit. 
+ If the calculated check digit is in the range 0 to 9, go to step 5.
+ If the calculated check digit is 10, continue with step 4.
#### 4. Re-calculate the check digit:
+ To each of the base number’s eight digits a secondary weight factor is 
assigned. From left to right these are: `7, 4, 3, 2, 5, 2, 7, 6`. 
+ Sum together the products of the weight factors and their associated 
digits. 
+ Divide the sum by 11. If the remainder is 0 then the calculated check digit 
is 0.
+ If the remainder is not 0 then subtract the remainder from 11, giving the 
00 calculated check digit. 
+ If the calculated check digit is 10, the IRD number is invalid.
#### 5. Compare the check digit:
+ Compare the calculated check digit to the last digit of the original IRD 
number. 
If they match, the IRD number is valid.

### Example 1
IR number `49091850`.

The base number is `4909185` and the supplied check digit is 0. 

The number is greater than `10,000,000.` Using the weightings above:

```
(0*3) + (4*2) + (9*7) + (0*6) + (9*5) + (1*4) + (8*3) + (5*2) = 154.
154 / 11 = 14 remainder 0 (i.e. mod (154,11) = 0)

The remainder (0) = check digit (0), so no further calculation is necessary.
```
### Example 2
IR number `35901981`.

The base number is 3590198 and the supplied check digit is 1. The number is greater than 
```
10,000,000. Using the weightings above:
(0*3) + (3*2) + (5*7) + (9*6) + (0*5) + (1*4) + (9*3) + (8*2) = 142.
142 / 11 = 12 remainder 10 (i.e. mod (142,11) = 10)
11 – 10 = 1 which matches the check digit.

The number is valid.
```

### Example 3
IR number `49098576`.

The base number is `4909857` and the supplied check digit is 6. The number is greater than `10,000,000`. Using the weightings above:

```
(0*3) + (4*2) + (9*7) + (0*6) + (9*5) + (8*4) + (5*3) + (7*2) = 177 .
177 / 11 = 16 remainder 1 (i.e. mod(177,11) = 1)
11 – 1 = 10 so perform the secondary calculation.
(0*7) + (4*4) + (9*3) + (0*2) + (9*5) + (8*2) + (5*7) + (7*6) = 181
181 / 11 = 16 remainder 5 (i.e. mod(181,11) = 5)
11 – 5 = 6, which matches the check digit.

The number is valid.
```
### Example 4 (9 digit IRD number)
IR number `136410132`.

The base number is `13641013` and the supplied check digit is 2. The number is greater than `10,000,000`. Using the weightings above:

```
(1*3) + (3*2) + (6*7) + (4*6) + (1*5) + (0*4) + (1*3) + (3*2) = 89 .
89 / 11 = 8 remainder 1 (i.e. mod (89,11) = 1)
11 – 1 = 10 so perform the secondary calculation.
(1*7) + (3*4) + (6*3) + (4*2) + (1*5) + (0*2) + (1*7) + (3*6) = 75
75 / 11 = 6 remainder 9 (i.e. mod (75,11) = 9)
11 – 9 = 2 which matches the check digit.

The number is valid.
```

### Example 5 (9 digit IRD number)
IR number `136410133`. 

The base number is `13641013` and the supplied check digit is 3. The number is greater than `10,000,000`. Using the weightings above:

```
(1*3) + (3*2) + (6*7) + (4*6) + (1*5) + (0*4) + (1*3) + (3*2) = 89 .
89 / 11 = 8 remainder 1 (i.e. mod (89,11) = 1)
11 – 1 = 10 so perform the secondary calculation.
(1*7) + (3*4) + (6*3) + (4*2) + (1*5) + (0*2) + (1*7) + (3*6) = 75
75 / 11 = 6 remainder 9 (i.e. mod (75,11) = 9)
11 – 9 = 2, which does not match the check digit (3).

The number is invalid.
```

### Example 6
IR number `9125568`. 

The number is less than `10,000,000` so fails the first validation.
The number is invalid.
