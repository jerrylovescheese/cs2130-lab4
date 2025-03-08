## Homework 4

TL; DR
**gcd.binary**
6B 01 6F 03 64 44 7D 82 20

84 02 07 68 10 6C 2F 77 51 5B 11 72 51 14 01 85 83

0B 0C 82 20 83
***

Let's just assume everything written in homework_3.md is correct.

gcd(a,b) = gcd(b, modulo(a,b))

1. Load the value in memory at address 0x01 into a register (r2)
**icode = 6, b = 3, register = r2**
01101011

6B 01

2. Load the value in memory at address 0x03 into a register (r3)
**icode = 6, b = 3, register = r3**
01101111

6F 03

3. r1 = memory of return
**icode = 6, b = 0, register = r1**
01100100

64 44

4. if r3 <= 0, pc = r1 (The greatest common divisor is smallest result seen before 0.)
**icdoe = 7, register = r3 & r1**
01111101

7D

5. call modulo, jump to 0x20 because that's where the modulo function codes start
**icode = 8, b = 2**
10000010

82 20

***
**mod.binary**
84 02 07 68 10 6C 2F 77 51 5B 11 72 51 14 01 85 83
***

6. r2 = r3
**icode = 0, register = r2 & r3**
00001011

0B

7. r3 = r0
**icode = 0, register = r3 & r0**
00001100

0C

8. if r3 <= 0, pc = r1 (The greatest common divisor is smallest result seen before 0.) if r3 > 0, go to step 9 and continue recursive calls (same as step 4)
**icdoe = 7, register = r3 & r1**
01111101

7D

9. call 20
**icode = 8, b = 2**
10000010

82 20

10. store e0 to r3 because e0 is where the end result should be
**icode = 6, b = 0, register = r3**
01101100

6C E0

11. write r0 to memory address at r3
**icode = 4 register = r0 & r3**
01000011

43

10. ret

83