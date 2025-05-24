Bit manipulation is a powerful technique that allows direct manipulation of individual bits of data. It is commonly used in competitive programming, embedded systems, cryptography, and performance-critical software.

---
## Basic Bitwise Operators in C++

| Operator | Name        | Description                                     | Syntax / Example                           | Time Complexity |
| -------- | ----------- | ----------------------------------------------- | ------------------------------------------ | --------------- |
| `&`      | AND         | Sets each bit to 1 if both bits are 1           | `a & b`                                    | O(1)            |
| \|       | \|          | OR                                              | Sets each bit to 1 if one of two bits is 1 | O(1)            |
| `^`      | XOR         | Sets each bit to 1 if only one of two bits is 1 | `a ^ b`                                    | O(1)            |
| `~`      | NOT         | Inverts all the bits                            | `~a`                                       | O(1)            |
| `<<`     | Left Shift  | Shifts bits to the left (multiplies by 2^n)     | `a << n`                                   | O(1)            |
| `>>`     | Right Shift | Shifts bits to the right (divides by 2^n)       | `a >> n`                                   | O(1)            |

---
## Common Bit Tricks

| Operation               | Code                        | Description                    |
| ----------------------- | --------------------------- | ------------------------------ |
| Check if `n` is even    | `n & 1 == 0`                | Last bit 0 → even              |
| Multiply by 2^k         | `n << k`                    | Fast multiplication            |
| Divide by 2^k           | `n >> k`                    | Fast division                  |
| Check if kth bit is set | `(num & (1 << k)) != 0`     | Returns true if kth bit is set |
| Set the kth bit         | `n = (1 << k)`              | Set the nth bit to 1           |
| Unset the kth bit       | `n & ~(1 << k)`             | Sets the kth bit to 0          |
| Toggle the kth bit      | `num ^= (1 << k)`           | Flips the kth bit              |
| Count set bits          | `__builtin_popcount(n)`     | Counts bits set to 1 in `n`    |
| Is power of 2           | `n > 0 && (n & (n-1)) == 0` | Only one bit is set            |
| Lowest set bit          | `n & -n`                    | Isolates lowest set bit        |
| Turn off lowest set bit | `n & (n - 1)`               | Useful in bit counting         |

> [!NOTE]
> `k` is 0-indexed from the right (LSB)** in all standard C++ bit manipulation.

---
## Sample Program Demonstrating All Operations

```cpp
#include <iostream>
#include <bitset>
using namespace std;

int main() {
    int a = 29;   // 11101
    int b = 23;   // 10111
    int pos = 2;

    cout << "a = " << bitset<8>(a) << " (" << a << ")\n";
    cout << "b = " << bitset<8>(b) << " (" << b << ")\n\n";

    cout << "AND (a & b): " << bitset<8>(a & b) << "\n";
    cout << "OR  (a | b): " << bitset<8>(a | b) << "\n";
    cout << "XOR (a ^ b): " << bitset<8>(a ^ b) << "\n";
    cout << "NOT (~a):    " << bitset<8>(~a) << "\n";
    cout << "Left Shift (a << 1): " << bitset<8>(a << 1) << "\n";
    cout << "Right Shift (a >> 1): " << bitset<8>(a >> 1) << "\n\n";

    // Bit position operations
    cout << "Check bit at pos 2 in a: " << ((a & (1 << pos)) != 0) << "\n";
    cout << "Set bit at pos 2: " << bitset<8>(a | (1 << pos)) << "\n";
    cout << "Unset bit at pos 2: " << bitset<8>(a & ~(1 << pos)) << "\n";
    cout << "Toggle bit at pos 2: " << bitset<8>(a ^ (1 << pos)) << "\n\n";

    // Advanced tricks
    cout << "Number of set bits in a: " << __builtin_popcount(a) << "\n";
    cout << "Is a power of 2? " << ((a & (a - 1)) == 0 ? "Yes" : "No") << "\n";
    cout << "Lowest set bit in a: " << bitset<8>(a & -a) << "\n";
    cout << "Turn off lowest set bit: " << bitset<8>(a & (a - 1)) << "\n";

    return 0;
}
```

#### Output

```SQL
a = 00011101 (29)
b = 00010111 (23)

AND (a & b): 00010101        
OR  (a | b): 00011111        
XOR (a ^ b): 00001010        
NOT (~a):    11100010        
Left Shift (a << 1): 00111010
Right Shift (a >> 1): 00001110

Check bit at pos 2 in a: 1
Set bit at pos 2: 00011101
Unset bit at pos 2: 00011001
Toggle bit at pos 2: 00011001

Number of set bits in a: 4
Is a power of 2? No
Lowest set bit in a: 00000001
Turn off lowest set bit: 00011100
```

---
## Bit Masking in C++

Bitmasking is a technique used in programming to perform operations more efficiently on binary data. Bitmasking is a frequently employed technique in algorithms to enhance performance in terms of time complexity, utilizing bitwise operators for efficient operations at the bit level.

Bitmasking in C++ involves manipulating individual bits of a number to achieve the desired output. It is achieved by generating a bit mask and is used very often for the following operations:

- **Bit Toggle:** If a bit is set to 0, it can be toggled to 1 and vice-versa.
- **Bit Setting:** If a bit is set to 0 then it's called 'bit is NOT set'. We can set it by performing a toggle operation and change it to 1. This is known as bit setting.
- **Bit Clearing:** If a bit is set to 1 then it's called a 'SET-BIT'. We can change it to 0 by performing a toggle operation this is called a - 'Bit-clearing' operation.
- **Checking specific bit is on or off:** A bit is said to be on if it's 1 and off if it's 0. For example, an integer can contain multiple bits and we can check if, in that integer, a specific bit is set or not by utilizing bitwise operators.

---
### What is a Bit Mask?

A bit mask is the fundamental technique to achieve bit masking. It is basically a binary pattern used to perform various bit-level operations like set, clear, toggle or checking if a bit is set or not.

The bit mask is created in the following way:
1. Assuming that we have the set of numbers, whose binary representation has 8 bits in it, we will use this as a reference.
   
   We know that 1 has only a single bit set to 1 which is the right-most bit otherwise known as the least significant bit. The remaining 7 bits are set to 0. So it would look something like this :
   
```SQL
Binary Representation of 1
0000 0001   (1)
```

2. Shifting the set bit (the LSB) to 3 places to the left using expression (1<<3) would look something like this:
   
```SQL
Binary Representation after shifting 3 places to left
0000 1000   (8)
```

3. After shifting, the set bit to 3 places, it becomes 8. Similarly, we can do this for any place. We'll use this shifting property in following bitwise techniques to create a bit mask and then perform various bitwise operations with it.

---
### Common Bit Masking Operations

| Operation                   | Purpose                          | Expression / Code  | Explanation                            |
| --------------------------- | -------------------------------- | ------------------ | -------------------------------------- |
| **Check if bit is 1**       | Test if the kth bit is set (1)   | `num & (1 << k)`   | Mask has 1 at kth bit, 0 elsewhere     |
| **Set bit**                 | Set the kth bit to 1             | `num = (1 << k)`   | Sets kth bit to 1                      |
| **Clear bit**               | Set the kth bit to 0             | `num &= ~(1 << k)` | AND with complement mask               |
| **Toggle bit**              | Flip the kth bit                 | `num ^= (1 << k)`  | XOR with mask having 1 at kth position |
| **Turn off lowest set bit** | Clears the rightmost set bit     | `num &= (num - 1)` | Fast way to remove LSB                 |
| **Isolate lowest set bit**  | Keeps only the rightmost set bit | `num & -num`       | Useful for bit iteration               |

---
### Bitmasking Operations in C++

#### **1. Setting a specific bit:**
Setting a specific bit basically means changing it from 0 to 1. It can be done by utilizing the Bitwise OR because of its property to give 1 if either of the bits is set to 1 and the bitwise left shift operator.

We will shift the LSB bit of 1 to the specified position that we want to set and then perform a bitwise OR Operation.
##### Syntax
```SQL
integer | (1 << bit_position_to_be_set)
```

> [!NOTE]
> Here, the bit position to be set will be the place of the bit that we want to change to 1.
##### Example
```SQL
Setting the 5-th bit of the input integer 11.

0000 1011    (11)
  OR(|)
0010 0000    (1 << 5)
-------------------------
0010 1011    (43)
```

#### **2. Clearing a Bit:**
Clearing a bit means we set it to 0 if it is 1 without touching or affecting any other bits. This is done by using Bitwise AND and the negation operator (Bitwise NOT). The Bitwise NOT flips all the bits that are 1 to 0 and 0 to 1. This property of the bitwise NOT helps us in clearing a set bit.
##### Syntax
```SQL
integer & ~(1 << bit_position_to_clear)
```

##### Example
```SQL
Clearing the 3-rd bit of the input integer 11.

0000 1011    (11)
  AND(&)
1111 0111    ~(1 << 3)
-------------------------
0000 0011    (3)
```

### **3. Toggle a Bit:
1 we make it 0 and if it's set to 0 then we flip it to 1. This is easily achievable by the Bitwise XOR operator (^) and the left shift (<<). We will utilize the property of the XOR operator to flip the bits if the bits of 2 different numbers are not the same.

The same approach is used that is, by shifting 1 to a specific position which we want to flip.
##### Syntax
```SQL
Integer ^ (1 << bit_position_to_toggle)
```

##### Example
```SQL
Toogling the 0-th bit of the input integer 11.

0000 1011    (11)
  XOR(^)
1101 1111    ~(1 << 0)
-------------------------
0000 1010    (10)
```

### **4. Check if a Bit is Set or not**
In this operation, we check if a bit at a specific position is set or not. This is done by using the bitwise AND (&) and the Left shift operator. We basically left shift the set bit of 1 to the specified position for which we want to perform a check and then perform a bitwise AND Operation.

If the bit is set then the answer will be - $2^{\text{(bit-position)}}$ For example, if the bit position is $3$, then the answer will be $2^3 = 8$. Else if the bit is $0$ (not set) then the answer will be $0$.
##### Syntax
```SQL
Integer & (1 << bit_position_to_check)
```

##### Example
```SQL
Checking if the 3-rd bit of the input integer 11 is set or not.

0000 1011    (11)
  AND(&)
0000 1000    (1 << 3)
-------------------------
0000 1000    (8)
```

---
## Sample Program

```cpp
#include <iostream>
#include <bitset>
using namespace std;

void printBits(int num, string label) {
    cout << label << " (" << num << ") : " << bitset<8>(num) << endl;
}

int main() {
    int num = 42; // Binary: 0010 1010
    int k = 2;    // Operate on 2nd bit from LSB (0-indexed)

    printBits(num, "Original");

    /* 1. Check if k-th bit is set */
    bool isSet = num & (1 << k);
    cout << "Is bit " << k << " set? " << (isSet ? "Yes" : "No") << endl;

    /* 2. Set k-th bit */
    int setBit = num | (1 << k);
    printBits(setBit, "After Setting bit 2");

    /* 3. Clear k-th bit */
    int clearBit = num & ~(1 << k);
    printBits(clearBit, "After Clearing bit 2");

    /* 4. Toggle k-th bit */
    int toggleBit = num ^ (1 << k);
    printBits(toggleBit, "After Toggling bit 2");

    /* 5. Isolate lowest set bit */
    int isolated = num & -num;
    printBits(isolated, "Lowest set bit isolated");

    /* 6. Turn off lowest set bit */
    int removedLSB = num & (num - 1);
    printBits(removedLSB, "After turning off lowest set bit");

    return 0;
}
```

#### Output

```SQL
Original (42) : 00101010
Is bit 2 set? No
After Setting bit 2 (46) : 00101110
After Clearing bit 2 (42) : 00101010
After Toggling bit 2 (46) : 00101110
Lowest set bit isolated (2) : 00000010
After turning off lowest set bit (40) : 00101000
```

---
## Properties of bitwise operations

Bit operations have many properties. Here, we will list common properties of AND, OR, XOR, and negation in bit operations. We assume that the variables below are all signed integers.

 1. **Idempotent law:**
$$
a \; \& \; a = a
$$
$$
a \; | \; a = a
$$

> [!NOTE]
>   note that XOR does not satisfy the idempotent law.

  
2. **Commutative law:** 
  $$
   a \; \& \; b = b \; \& \; a
 $$
  $$
   a \; | \; b = b \; | \; a
 $$
 $$
   a \; ⊕ \; b = b \; ⊕ \; a
 $$
  
  
3. **Associativity:**
  $$
   (a \; \& \; b) \; \& \; c \; = \; a \; \& \; (b \; \& \; c)
 $$  $$
   (a \; | \; b) \; | \; c \; = \; a \; | \; (b \; | \; c)
 $$
$$
   (a \; ⊕ \; b) \; ⊕ \; c \; = \; a \; ⊕ \; (b \; ⊕ \; c)
 $$
  
4. **Distributive Law:**
  $$
   (a \; \& \; b) \; | \; c \; = \; (a \; | \; c) \; \& \; (b \; | \; c)
 $$  $$
   (a \; | \; b) \; \& \; c \; = \; (a \; \& \; c) \; | \; (b \; \& \; c)
 $$
  $$
   (a \; ⊕ \; b) \; \& \; c \; = \; (a \; \& \; c) \; ⊕ \; (b \; \& \; c)
 $$

5. **De Morgan's Law:**
 $$
   \sim(a \; \& \; b) \; = \; (\sim a) \; | \; (\sim b)
$$
$$
   \sim(a \; | \; b) \; = \; (\sim a) \; \& \; (\sim b)
$$  
6. **Negative operation properties:**
   $$
   -1 \; = \;\; \sim 0
   $$
   $$
   -a \; = \; \; \sim(a - 1)
   $$

7. **AND operation properties:**
   $$
   a \; \& \; 0 \; = \; 0
   $$
   $$
   a \; \& \; (-1) \; = \; a
   $$
   $$
   a \; \& \; (\sim a) \; = \; 0
   $$
  
8. **OR operation properties:**
   $$
   a \; | \; 0 \; = \; a
   $$
   $$
   a \; | \; (\sim a) \; = \; -1
   $$
  
9. **XOR operation properties:**
  $$
  a \; ⊕ \; 0 \; = \; a
  $$
  $$
  a \; ⊕ \; a \; = \; 0
  $$

10. **Other properties:**
    - The result of $a \; \& \; (a−1)$ is to change the last bit with value 1 in the binary representation of `a` to 0.
    - The result of $a \; \& \; (-a)$ ( equivalent to $a \; \& \; (\sim(a−1))$ ) is to keep only the last 1 of the binary representation of `a`, and set the remaining 1s to 0.
    - Using these properties, many bit operation problems can be solved strategically.
      
---
## Use Cases of Bit Masking

1. **Subset Generation** (for size `n`, bitmask from `0` to `2^n - 1`)    
2. **Permission Flags** (each bit represents a permission/state)
3. **Efficient Storage** (store multiple Boolean flags in one variable)
4. **Fast Lookup** (toggle states efficiently)
5. **Dynamic Programming on Bitmask** (like in the Travelling Salesman Problem)

---
## Sample Interview Questions

1. **Check if a number is a power of 2.**
2. **Count number of 1’s in binary representation.**
3. **Generate all subsets of a set using bitmasks.**
4. **Find the single number that appears once in an array where others appear twice.**
5. **Check if two integers have opposite signs.**
6. **Swap two numbers without using a temporary variable.**

```cpp
// XOR Swap Example
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

---
