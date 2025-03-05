# Task: Pack and Ship -

## Challenge Overview
The GDSC Tech Team mistakenly left sensitive data in their latest binary release and attempted to protect it with basic obfuscation. Our task was to evaluate the security of their approach and recover the hidden flag.

### Files Provided
- *Binary Release*
- *SHA256 Checksum*: 56548282b3d968e12d14c0760fc2ac778d5a9bc9f10c78d1c8233aa97f5b7329
- *Flag Format*: gdsc{...}

---

## Approach to Solve the Challenge

### Step 1: Download and Verify the Binary
First, we downloaded the provided binary and verified its integrity using the SHA256 checksum:
bash
sha256sum unpacking

The output should match the provided checksum to ensure that the file was not altered.

### Step 2: Grant Execution Permission
Before running the binary, we needed to grant it execution permissions:
bash
chmod +x unpacking


### Step 3: Running the Binary
Running the binary prompted us to enter a password:
bash
./unpacking
Enter the password:


### Step 4: Analyzing the Binary
Since the binary was protected with basic obfuscation, we used the following approaches to analyze it:

#### 4.1 Strings Analysis
We checked for any embedded strings using the strings command:
bash
strings unpacking | less

This often reveals hardcoded passwords, messages, or hints within the binary.

#### 4.2 Reverse Engineering with Ghidra/IDA
We loaded the binary into Ghidra to analyze its functions and identify how the password was verified.

- We found that the binary contained a hardcoded password: bt8uA1uxF350yZLuto9GmqTWJBpP2jUq.
- The program compared this password to user input before revealing the flag.

#### 4.3 Debugging with GDB
Alternatively, we used gdb to set breakpoints and inspect memory during execution:
bash
gdb ./unpacking
break *main
run

This helped confirm the password validation process.

### Step 5: Retrieving the Flag
Once we discovered the password, we executed the binary and provided the correct password:
bash
./unpacking
Enter the password: bt8uA1uxF350yZLuto9GmqTWJBpP2jUq
Correct password! Here is the flag: gdsc{unp4ck1n6_b1n4r135_15_n4u6h7y}


---

## Conclusion
The flag was successfully retrieved using reverse engineering techniques such as strings analysis, static analysis with Ghidra, and debugging with GDB. The challenge demonstrated the importance of securing sensitive information within binaries, as simple obfuscation can be easily bypassed.

### *Recovered Flag:*
plaintext
gdsc{unp4ck1n6_b1n4r135_15_n4u6h7y}
