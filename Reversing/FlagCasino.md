# FlagCasino

## Challenge Description
The team stumbles into a long-abandoned casino. As you enter, the lights and music whir to life, and a staff of robots begin moving around and offering games, while skeletons of prewar patrons are slumped at slot machines. A robotic dealer waves you over and promises great wealth if you can win - can you beat the house and gather funds for the mission?

## Tools Used
- IDA Pro (Freeware)
- Kali Linux
- Python
- C programming language (for a test script)
## Steps to Solve the Challenge

### Step 1: Analyzing the Binary in IDA Pro

1. **Load the binary in IDA Pro**:
    
    - Open the `casino` binary in IDA Pro to analyze its disassembled code.
2. **Locate the `check` array**:
    
    - The `check` array contains the values that the generated random numbers must match.
    - The values in the `check` array were found at a specific data section in the binary.
    - Extract these values and interpret them as 32-bit integers.
    - 
![[flag_casino_IDA.png]]
3. **Understand the `main` function logic**:
    
    - The main function reads input, seeds the random number generator, and compares generated random numbers against the `check` array values.
    - The goal is to find the input values that, when used as seeds, generate the expected random numbers.
![[flag_casino_IDA_2.png]]
### Step 2: Create a Test Script to Understand `rand()` Behavior
1. **Write a C script to understand the behavior of `srand` and `rand` functions**:
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    for (int seed = 0; seed < 256; seed++) {
        srand(seed);
        printf("Seed: %d, Rand: %d\n", seed, rand());
    }
    return 0;
}
```
2. **Compile and run the script**:
```sh
gcc -o rand_test rand_test.c
./rand_test > rand_output.txt
```

3. **Analyze the output**
    - This script helps understand which seeds produce which random values.

### Step 3: Brute Force the Correct Seeds
1. **Create a Python script to brute force the correct seeds**:
```python
import ctypes

# These are the raw bytes extracted from the check array in the binary.
# The values need to be interpreted correctly as 32-bit integers.
check_bytes = [
    0x0BE, 0x28, 0x4B, 0x24,
    0x05, 0x78, 0xF7, 0x0A,
    0x17, 0xFC, 0x0D, 0x11,
    0xA1, 0xC3, 0xAF, 0x07,
    0x33, 0xC5, 0xFE, 0x6A,
    0xA2, 0x59, 0xD6, 0x4E,
    0xB0, 0xD4, 0xC5, 0x33,
    0xB8, 0x82, 0x65, 0x28,
    0x20, 0x37, 0x38, 0x43,
    0xFC, 0x14, 0x5A, 0x05,
    0x9F, 0x5F, 0x19, 0x19,
    0x20, 0x37, 0x38, 0x43,
    0x80, 0x93, 0x14, 0x63,
    0x99, 0xB2, 0x5A, 0x61,
    0x33, 0xC5, 0xFE, 0x6A,
    0xB8, 0xCF, 0x6F, 0x6C,
    0x20, 0x37, 0x38, 0x43,
    0x37, 0xA2, 0x3D, 0x0F,
    0x33, 0xC5, 0xFE, 0x6A,
    0x99, 0xB2, 0x5A, 0x61,
    0xB8, 0x82, 0x65, 0x28,
    0xFC, 0x14, 0x5A, 0x05,
    0x94, 0x49, 0xE4, 0x3A,
    0xE9, 0xDF, 0xD7, 0x06,
    0xA2, 0x59, 0xD6, 0x4E,
    0xCD, 0x4A, 0xCD, 0x0C,
    0x64, 0xED, 0xD8, 0x57,
    0x99, 0xB2, 0x5A, 0x61,
    0x2A, 0xBC, 0xE9, 0x22
]

# Convert these bytes into 32-bit integers (little-endian)
check_values = []
for i in range(0, len(check_bytes), 4):
    value = check_bytes[i] | (check_bytes[i + 1] << 8) | (check_bytes[i + 2] << 16) | (check_bytes[i + 3] << 24)
    check_values.append(value)

libc = ctypes.CDLL('libc.so.6')

def brute_force_seed(target, max_seed=1000000):
    for seed in range(max_seed):
        libc.srand(seed)
        rand_value = libc.rand()
        if rand_value == target:
            return seed
    return None

correct_inputs = []
default_seed = 1  # Using a default seed value for missing seeds
for value in check_values:
    seed = brute_force_seed(value, max_seed=1000000)
    if seed is not None:
        correct_inputs.append(seed)
    else:
        correct_inputs.append(default_seed)
        print(f"Could not find a seed for value {value}, using default seed {default_seed}")

print("Correct inputs found:")
print(" ".join(chr(i) for i in correct_inputs))

input_string = "".join(chr(i) for i in correct_inputs)
print(f"Input string: {input_string}")

```

2. **Run the script to find the correct input string**:
```sh
python3 brute_force.py
```

3. Analyze the output:
	*  The script should print the input string that needs to be fed into the `casino` binary.
	```sh
	Correct inputs found:
H T B { r 4 n d _ 1 s _ v 3 r y _ p r 3 d 1 c t 4 b l 3 }
Input string: HTB{r4nd_1s_v3ry_pr3d1ct4bl3}
	```

Which was our flag!

