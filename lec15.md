# Lec 15 Integers

Answer is the correct answer modulo 2^bitsize

Division usually don't cause overflow.

Except for one case: `-2^31 / -1 = -2^31` underflow/overflow, as 2^31 is not in range.

The result Java give you is everything after throwing away the top bit (8th). Easy for the hardware.

Java ignores the left side of the bar.



1 = 00000001

-1 = 11111111

-2 = 11111110

any negative number: first bit is always 1

0 = 1|00000000 = 00000000

127 = 01111111 



On unsigned types (char), arithmetic is the same. Instead of -1, 2^pow - 1



### Conversion

When we do Object type casting, we do not change the Object and only let the compiler know.

In integer casting, result of casting actually changes value.

Case of integers assigining. One of them has to be shorter narrower than the other.

`aShort = aByte` valid as all values of Byte are in range of Short. Not the other way around.

Implicit coersion. 

If do not loose information, just assign.

If you might loose information, you can force using `(byte)`.



OK. aByte = 13;  aByte = 12 + 100; Compiler will let it go.



### Promotion

When we add Integers, if neither is `long`, convert them into `int`.

If one of them is not the `bigger type` convert to that type.

aByte + 3 == (int) aByte + 3

aLong + 3== along + (long) 3

'A' + 2 == (int) 'A' + 2

aByte = aByte + 1 (byte assigned to integer, might loose information)

But fortunately: aByte += 1. Underneath, aByte = (byte) aByte + 1.



Checking for overflow is a pain.



### Bit Twiddling

**Bitwise operations**

Java allow for handling integer types as sequences of bits.

Mask `&`  and

Set `|` or

Flip `^` exclusive or, unequal, add and throw away carry for base 2

Flip all `~`  compliment, like not



**Shifting**

Left shift `<<`. Shift things over. Anything falls of the left end get throw away.

Arithmetic Right `>>`. Shift things over, but copies signed. 

Logical Right `>>>`: 000s copied over. Rest thrown away.

-1 >>> 29 = 7 (3 1s in the end)
Ints are 32 bits, shift by 29, leave 3 bits in the end. 2^2 + 2 + 2^0 = 4+2+1=7

x << n = x*2^n

x >> n = [x/2*n] rounded down

((1 << 5) - 1)  5- bit integer, bits 3-7 of x (extract 5 bit integer)

