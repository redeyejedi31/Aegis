# **Project Aegis: Password Safety Checker**

I follow strict password best practices. My passwords are long, complex, and unique, containing a robust mixture of letters, numbers, and special characters. I never reuse the same password across different accounts. However, this does not stop threat actors from actively targeting systems, and like many of us, I frequently receive reports warning me that some of my online accounts may have been compromised in historical data leaks.

Checking several hundred unique passwords one by one is an incredibly tedious, time consuming task. I needed a way to audit my entire vault quickly and privately.

Developed with the collaborative support of artificial intelligence, Project Aegis was created to solve this exact problem. It saves a massive amount of time by allowing you to check your entire list at once, directly from your computer.

## **⚠️ VITAL SECURITY WARNING**

Before you begin, you must understand that handling your password files requires absolute caution:

* **DO NOT use this on public networks:** Never run this tool on a public, shared, or open Wi Fi network. Only use it in your own safe, private, and trusted home network.  
* **Work in isolation:** Ensure you run this check on a personal device that is fully secure.  
* **Delete files immediately:** After you complete your audit, you must permanently delete any unencrypted password files you exported from your computer and empty your recycle bin immediately. Leaving plaintext password spreadsheets on your hard drive is a catastrophic security risk.

## **🔒 How does Project Aegis keep you safe?**

Unlike other online tools that require you to upload your passwords to their servers, **Project Aegis keeps your raw data completely private.**

Here is how it works in plain English:

1. **Local Protection:** The moment you load your password list into Aegis, your computer immediately translates each password into a scrambled string of letters and numbers called a cryptographic hash.  
2. **Anonymous Querying:** Aegis only sends the first five letters of that scrambled string to the secure breach registry. This tiny snippet is completely anonymous, and it is mathematically impossible for anyone to reconstruct your password from it.  
3. **Private Comparison:** The registry sends back a list of compromised codes starting with those same five letters. Your browser then compares your passwords against that list locally inside your browser memory.

At no point does your real password ever leave your machine.

## **🔬 Step by Step Example: Testing "hello world"**

To see exactly how your private data is protected, let us trace what happens under the hood if you were to check the password **"hello world"**:

### **Phase A: Local Scrambling**

The browser takes your password and calculates its unique cryptographic signature using the SHA 1 algorithm.

* **Plaintext Password:** hello world  
* **Scrambled Signature:** 2AAE6C35C94FCFB415DBE95F408B9CE91EE846ED

This signature is completely unique to your password. However, Aegis will not send this entire code over the internet.

### **Phase B: Slicing the Code**

The application splits this forty character signature into two distinct parts:

* **The Routing Prefix (The first five characters):** 2AAE6  
* **The Private Suffix (The remaining thirty five characters):** C35C94FCFB415DBE95F408B9CE91EE846ED

### **Phase C: The Anonymous Inquiry**

Aegis sends only the five character prefix (2AAE6) to the secure Have I Been Pwned database. Because millions of different passwords generate signatures starting with those same five letters, the database server has absolutely no way of knowing which password you are checking.

To retrieve the matching records, the browser queries this exact public API endpoint:

👉 https://api.pwnedpasswords.com/range/2AAE6

The database looks up its records and sends back a list of all compromised suffixes that share our exact prefix. To save bandwidth, the server only returns the remaining suffixes.

The raw API response matches this structured table:

| Returned Suffix from API (35 Characters) | Exposure Count |
| :---- | :---- |
| 001D6E799D79FEE2D16C374D6CFA0DA89A89 | 1 |
| 01DFBE61661D79E7FA3A849B45C4197EFB3 | 4 |
| C35C94FCFB415DBE95F408B9CE91EE846ED | 583274 |
| F9A27F1CD86C1D04FAEF32E7B165BC48A04 | 12 |
| FDF863B8B8E85E8687D2FA6ED56D9F36965 | 85 |

*(Note: To save bandwidth, the real database only transmits the raw suffix list over the network, and your browser automatically prepends the prefix locally in your machine memory).*

### **Phase D: The Local Match & Reconstruction**

Now, completely inside your browser memory, Aegis processes the response. To perform a secure lookup, it temporarily recombines your prefix with each downloaded suffix.

Here is how the matching process looks inside your active browser memory:

| Reconstructed Hash in RAM | Leak Count | Status Indicator |
| :---- | :---- | :---- |
| \[2AAE6\]001D6E799D79FEE2D16C374D6CFA0DA89A89 | 1 |  |
| \[2AAE6\]01DFBE61661D79E7FA3A849B45C4197EFB3 | 4 |  |
| \[2AAE6\]C35C94FCFB415DBE95F408B9CE91EE846ED | 583274 | ★ **MATCH DETECTED\!** |
| \[2AAE6\]F9A27F1CD86C1D04FAEF32E7B165BC48A04 | 12 |  |
| \[2AAE6\]FDF863B8B8E85E8687D2FA6ED56D9F36965 | 85 |  |

Aegis instantly flags your password as **Compromised** because the reconstructed signature matches your local hash exactly.

## **🚀 How to Run the Portable Version (No Installation Required)**

This is the simplest way to run the tool without needing any technical setup:

1. Download the aegis.html file from this repository.  
2. Save it to a private folder on your computer.  
3. Double click aegis.html to open it instantly in your web browser.  
4. Go to the **Bulk CSV Audit** tab, paste or drag in your exported password list, map your columns, and click **Deploy Diagnostics Matrix** to begin.

## **🛡️ License**

This project is open source and released under the MIT License.