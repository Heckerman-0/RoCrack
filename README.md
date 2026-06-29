# RoCrack ⛏️ Roblox Password Cracker
This Python script automates the process of brute-forcing passwords against a specified Roblox account endpoint using an external wordlist attack. It is designed to efficiently test dictionary passwords until a valid login combination is found.

**License:** Public Domain (No explicit license file needed!)

---

## 🚀 Features
*   **Wordlist Driven:** Reads potential passwords from a specified text file (`RockYou.txt`).
*   **API Integration:** Interacts directly with the Roblox authentication API endpoint for real-time testing.
*   **Progress Tracking:** Uses `tqdm` for a clear and updating visual count of which password is currently being tested.
*   **Robust Error Handling:** Includes comprehensive `try...except` blocks to gracefully handle network issues, timeouts, HTTP errors, and JSON decoding failures.

## 🛠️ Setup &amp;amp;Installation
### Prerequisites
You must have Python installed on your system.

### Installation Steps
This script relies on several external libraries. Install them using pip:

```bash
pip install requests tqdm
File Structure
Your project directory should be structured exactly as follows:

/RoCrack
├── password_cracker.py  # <-- The main Python script
├── RockYou.txt          # <-- Your dictionary file (the wordlist)
└── README.md            # <-- This documentation file
Tip for Wordlist Quality: Remember that the quality of this tool is entirely dependent on the RockYou.txt file you provide! Remember to source your own comprehensive list.

⚙️ Configuration &amp;Usage
Step 1: Update Variables (Crucial!)
Open password_cracker.py and manually update these variables at the top of the script:

username = "TargetUsername" : <-- CHANGE THIS to the actual Roblox username!
wordlist_path = "RockYou.txt" : <-- Ensure this points correctly to your wordlist file!
Step 2: Run the Script
Execute the main Python file from your terminal:

python password_cracker.py
The script will begin testing passwords immediately, displaying a live count in the console.

🔬 How It Works (Under the Hood)
Wordlist Loading: The read_wordlist function loads all potential passwords from RockYou.txt, stripping any extraneous whitespace or newlines.
Testing Loop: The script iterates over every word, calling attempt_login() for each one.
API Interaction: attempt_login() sends a secure POST request to the Roblox authentication endpoint (https://auth.roblox.com/v2/login) containing the credentials in JSON format.
Success Validation: The function doesn't just trust the HTTP status code; it attempts to parse the JSON response body. It is designed to check for a specific success indicator provided by Roblox (currently checking data.get("success")). If this key/value pair confirms success, the attack stops immediately.
Pacing: A mandatory pause of 0.5 seconds (time.sleep(0.5)) is enforced between attempts to maintain good etiquette and avoid potential rate-limiting issues with Roblox servers.
🆘 Troubleshooting &amp; Known Issues
Follow these steps sequentially if the script fails or performs poorly:

1. Initial Setup Failures
Error: FileNotFoundError when running the script. Fix: Verify that RockYou.txt exists in the same directory as password_cracker.py, OR update wordlist_path to point to its correct absolute path.

Error: Script hangs or prints vague connection errors. Fix: Check your internet connection, or if you are behind a strict firewall/VPN, ensure that external outbound connections to Roblox's services are allowed on port 443 (HTTPS).

2. Login Logic Failures (Most Common)
Issue: The script runs, prints "FAILURE" for every word, and never finds the correct password, even though you know the password works. Cause: This is almost always an API Change. Roblox updates its backend endpoints frequently. Your current success verification logic inside attempt_login might be outdated. Fix (Advanced): You must inspect the successful response payload structure manually using a tool like Postman or by temporarily printing data in the script when you know it's logged in, and then update this line:

if data.get("success") is True: # <-- Update 'success' key if Roblox changes it!
    # ... success code
3. Performance &amp; Rate Limiting
Issue: The script runs very slowly, or sometimes fails intermittently during heavy usage. Fix: While the current time.sleep(0.5) is a good baseline, if you hit temporary rate limits, consider reducing the speed (i.e., increasing time.sleep() to 1 second) or implementing parallel processing for faster checks.

✨ Get Started
Make sure your wordlist is ready, update the username, and run the script! Good luck cracking those passwords!

