## Homework 3

```Java
public static void main (String[] args) {
    System.out.println("No one mourns the wicked");
}
```
**new in homework 4** 

Instead of needing to read the immediate values at bytes 0x01 and 0x03, it can assume the two values are already stored in registers 2 and 3 (respectively).

You should save the contents of register 1, since it should be unchanged when your function returns. Just before returning, save the value back to register 1.

So let's push r1 and pop it before returning.

* push r1
**reserve_bit = 1, icode = 0, b = 0**
10000100

84

* r0 = r2
**icode = 0**
00000010

02

* r1 = r3
**icode = 0**
00000111

07

* construct r2 as a loop initiation signal
**icode = 6, b = 0**
01101000

68 10
(the second number here is random)

* is r1 0? cause if it is let's just end the conversation and pc = r2
**icode = 7**
01110110

76

* turn r0 negative
**icode = 5, b = 1**
01010001

51

* r2 is where pc goes when loop should restart, so r2 = pc
**icode = 5, b = 3**
01011011

5B

* r0 += r1
**icode = 1**
00010001

11

* if r0 <= 0, pc = r2
**icode = 7**
01110010

72

* NOT DONE YET! What we have here is NOT the remainder - it's the divisor minus the remainder. 
* divisor - remainder = what we have (r0), then
* divisor - what we have (r0) = remainder.
* So we have to turn r0 back negative...
**icode = 5, b = 1**
01010001

51

* ... and we also have to add the divisor back!
**icode = 1**
00010100

14

* so now, the remainder is in r1.

* **new in homework 4** since the result of any function should be r0 we should make r0 = r1
**icode = 0**

00000001

01

* pop r1
**reserved_bit = 1, icode = 0, b = 1**
10000101

85

* return
**reserved_bit = 1, icode = 0, b = 3**
10000011

83