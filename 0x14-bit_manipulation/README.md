Bit manipulation

1. Bit Manipulation Lecture 3

2. Having gained good knowledge about the binary and hexadecimal and their interconversion system, we are good to start with the new concept of Bitwise operators in Embedded C A bitwise expression is used when we want to modify a variable by changing some or any of the individual bits of the variable. A bitwise operator is often confused with boolean operator. A boolean is used when we want to compare any two quantities with a condition. If the condition is satisfied ,it return a 1 else 0. Boolean operators are: && (logical and), || (logical or), ! (logical not). X && Y returns TRUE only if both X and Y are TRUE. X || Y returns TRUE if either X or Y are TRUE.

3. Bitwise operators 1. Bitwise AND (&) operator compare two bits and return 1 if both bits are set (1), otherwise return 0. 2. Bitwise OR (|) operator compare two bits and return 1 if any of them or both bits are set (1), otherwise return 0. 3. Bitwise XOR (^) operator compare two bits and return 1 if either of the bits are set (1), otherwise return 0. 4. Bitwise complement (~) operator takes single operand and invert all the bits of the operand. 5. Bitwise right shift (>>) operator insert 0 bit at most significant bit and shift subsequent bits to right. 6. Bitwise Left shift (<<) operator insert 0 bit at least significant bit and shift subsequent

4. Bitwise Operations

5. Right Shift Operator (>>) ● There are two shift operators – Left shift and Right shift. ● These operators shift the bits by the corresponding value, in other words move the bits. ● The right shift moves the bit to the right side of the LSB. int C = 0x45; int D = C>>2; printf(“value of D :%d”,D); 0 1 0 0 0 1 0 1 0 0 0 1 0 0 0 1 Output: Value of : 17

6. Example for right shift operator ● Want to divide a number by 2 quickly. ● Here you go, use bitwise right shift operator to divide an integer by 2. ● Each right shift operation reduces the number (operand) to its half. 1 0 0 0 1 0 0 0 0 1 0 0 0 1 0 0 0 0 1 0 0 0 1 0 0 0 0 1 0 0 0 1 0x88 = dec 136 0x88>>1 = 0x44 = dec 68 0x44>>1 = 0x22 = dec 34 0x22>>1 = 0x11 = dec 17

7. Simple program on right shift operator #include <stdio.h> int main() { int a = 24; // Use bitwise right shift to divide // number by power of 2 printf("24 / (2^1) => %dn", (a >> 1)); printf("24 / (2^2) => %dn", (a >> 2)); printf("24 / (2^3) => %dn", (a >> 3)); return 0; } Output : 24 / (2^1) => 12 24 / (2^2) => 6 24 / (2^3) => 3 As Ints As Bits 24>>1 == 12 11000>>1 == 1100 24>>2 == 6 11000>>2 == 0110 24>>3 == 3 11000>>3 == 0011

8. Left Shift Operator (<<) ● The left shift operator move the bits to the left side corresponding to the value. ● And similar to the Right shift operator,On applying left shift operator, the value multiplies by 2. int C = 0x45; int D = C<<2; printf(“value of D :%d”,D); 0 1 0 0 0 1 0 1 0 0 0 1 0 1 0 0 Output: Value of : 276 0 1 0x45 0x114

9. In the same program instead of int, if variable d is declared as char, then the value of d is 0x14 or 20 in decimal. Since the char is allocated only 8 bits in the memory , the extra bits in MSB will be lost on performing the left shift operator. int C = 0x45; char D = C<<2; printf(“value of D :%d”,D); 0 1 0 0 0 1 0 1 0 0 0 1 0 1 0 0 Output: Value of D: 20 0x45 0x14

10. Bitwise &(AND) AND compares each bit and returns 1 if the two bits are 1 (TRUE) otherwise 0 (FALSE) 00111011………………..(A=0x3B) & 10010110………………..(B=0x96) 00010010…………....(A&B=0x12) Simple example: We can find whether a number is odd or even using bitwise AND operator. int a = 25; int b = 30; if(a&1) printf(“a is an odd number”); else printf(“a is an even number”); if(b&1) printf(“b is an odd number”); else printf(“b is an even number”);

11. AND operator are used for extracting bits. Bitwise AND is a really really useful tool for extracting bits from a number--you often create a "mask" value with 1's marking the bits you want, and AND by the mask. Consider that in a 16 bit number 0x8EAB, you got to extract bits from position 6 through 12, extract 6 bits from a 16 bit number, how will you do it? Monitoring Specific Bit Monitoring specific bit in register is very important. In Embedded programming, very often we need to read status of flag bit in hardware register. These flag bit controls or indicate hardware feature. Also they are every useful while reading, writing data to and from microchip. So we continuously monitor these bits in register to carry out desired function by microchip. Let’s say if we want to monitor 4th bit for any change, we’ll write function as below: while( bits & (1<<4) ) // monitor for 4th bit changing from 0 to 1 { ....... ....... }

12. So, Now what is the binary form of 0x8EAB 1 0 0 0 1 1 1 0 1 0 1 0 1 0 1 1 Bits to extract , 6 through 12 To extract these particular bits, they have to masked with AND 1 and rest of the bits with AND 0, So the hex value for the masking number is 0 0 0 1 1 1 1 1 1 1 0 0 0 0 0 0 1 F C 0 So, the masking hex value 0x1FC0

13. & 1 0 0 0 1 1 1 0 1 0 1 0 1 0 1 1 ( 0x8EAB & 0x1FC0)>>6 0 0 0 1 1 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 1 1 1 0 1 0 0 0 0 0 0 0 Extracted bits , 6 through 12 0 0 0 0 0 0 0 0 0 0 1 1 1 0 1 0 After shifting the bits

14. Bitwise |OR) Bitwise OR is used for setting bits either high(1) or low(0): We often use variable to store boolean flag values e.g. isEven, isMarried, isPrime etc. Instead of wasting 4 byte to store single flag. You can use bit masking to store multiple flag values in single variable. A 4 byte unsigned integer can store 32 flags. We use bitwise OR | operator to set flag. To unset or check flag status we use bitwise AND & operator. At a high level it is known as bit masking, but you can think it as set, unset and check a bit status. OR will return a 1 if there is a 1 in either value at that bit. So: C = A | B; 00111011 | 10010110 10111111 The value of C will be 0xBF or in binary 10111111

15. Example : In the below code, we will set 2 flag status, one for visa eligibility in 0th bit and married status in 1st bit, and then we will change the married to unmarried status. int bits; //assigning a 32 bit variable bits = bits | (1<<0); // setting visa eligibility to 1 bits = bits | (1<<1); // setting marriage status to 1 printf("HEX : %xn",bits); if(bits &1){ printf("nYou are eligible to apply for VISAn");} else{ printf("nYou are not eligible to apply for VISAn");} if(bits &2) { printf("nYou are marriedn");} else{ printf("nYou are unmarriedn");} bits = bits&(~(1<<1)); printf("HEX : %xn",bits); if(bits &2){ printf("nYou are marriedn");} else{ printf("n You are unmarriedn");}

16. XOR (^ in C – Exclusive OR) XOR will return a 1 if there is a 1 at that bit for either value but not both. For example, if bit position 5 for both values has a 1 then XOr returns a 0. But if only one has a 1 and the other has a 0 XOR returns a 1. So: C = A^B; The value of C will be 0xAD or in binary 10101101. 00111011………………..(A=0x3B) ^ 10010110………………..(B=0x96) 10101101 **XOR is short for eXclusive-OR. By definition of XOR , the result will be a '1′ if both the input bits are different and result will be '0′ if both are same . XOR can be used to check the bit difference between 2 numbers.

17. int a = 10; int b=10; int c=30; int d; d= a^b; if(d==0) { printf("%d : A and B are equaln",d); } else { printf("%d : A and B are not equaln",d); } d = b^c; if(d==0) { printf("%d : C and B are equaln",d); } else { printf("%d : C and B are not equaln",d);}

18. Not(~) operator This returns the compliment of a value. This mean where there was a 0 there will now be a 1 and vice versa. So: C = ~(A); ! 00111011………………..(A=0x3B) 11000100………………..(C=0xC4)

19. Let’s say we have variable called REG and we have asked to set the bit-6. This can be achieved by writing this code. int REG = 0x8F; //binary form : 10001111 int DEG = 0x8F; int MASK = 0x40; printf("REG 1 : %x", REG); printf("nDEG 1 : %x", DEG); REG = REG | 0x40 ; // setting the sixth bit 01000000 DEG |= (1<<6); printf("nREG 2 : %x", REG); printf("nDEG 2 : %x", DEG); Setting and Inverting bits Inverting bits : Inverting (toggling) is accomplished with bitwise-XOR. In following, example we’ll toggle bit-6. REG^= (1 << 6) ; /* toggle bit 6 */

20. Testing bits Form a mask with 1 in the bit position of interest, in this case bit-6. Then bitwise AND the mask with the operand. The result is non-zero if and only if the bit of interest was 1: if ((bits & 64) != 0) /* check to see if bit 6 is set */ Same as: if (bits & 0x64) /* check to see if bit 6 is set */ Same as: if (bits & (1 << 6)) /* check to see if bit 6 is set */

21. Clearing bits Let’s say if we want to clear bit-7. This can be accomplished using bitwise-AND operator Mask must be as wide as the operand! if bits is a 32-bit data type, the assignment must be 32- bit:

22. Thank You !!!!!!!!!!!


