# How to Protect Your Code

This is a practical guide on how to secure your games and software against tools like Cheat Engine, dnSpy, and x64dbg. 

### 1. Hide Critical Values (Anti-Cheat Engine)
Never store important values like gold, health, or timers as plain data in memory. If your health is 100 and you save it as 100, any memory scanner will find it and change it in seconds.
* What to do: Obfuscate the value using basic math or a XOR mask before saving it to RAM. It must look like random data. Convert it back to the real value only for a split second when the application performs a calculation, then hide it again.

### 2. Encrypt Sensitive Strings (Anti-dnSpy / x64dbg)
Reverse engineers always look for specific words in your binary file, such as "Success", "Premium", or "Wrong Password". If these strings are visible in plain text, hackers will instantly locate your security checks and bypass them.
* What to do: Never leave important text unprotected. Store your secret strings as encrypted byte arrays. Decrypt them in memory only when the application needs to use them, and clear the memory buffer immediately after.

### 3. Confuse the Analyst (Smart Defense)
If your program detects an active debugger (like x64dbg), do not close the application immediately. A sudden crash tells the hacker exactly where your defense mechanism is triggered.
* What to do: If you detect a reverse engineer, change the program behavior quietly. Feed the debugger fake memory values, trigger silent errors, or delay execution. This confuses the analyst and wastes their time.

### 4. Check for Memory Patches
Hackers often modify your code directly inside the RAM while the app is running. For example, they can patch your assembly instructions to turn a "false" check into a "true" check.
* What to do: Implement background checks that calculate the checksum of your application code in real-time. If someone modifies a single byte of your code, the checksum will change, and the application will know it was tampered with.
