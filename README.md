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
* **Scrambled Signature:** 2aae6c35c94fcfb415dbe95f408b9ce91ee846ed

This signature is completely unique to your password. However, Aegis will not send this entire code over the internet.

### **Phase B: Slicing the Code**

The application splits this forty character signature into two distinct parts:

* **The Routing Prefix (The first five characters):** 2aae6  
* **The Private Suffix (The remaining thirty five characters):** 35c94fcfb415dbe95f408b9ce91ee846ed

### **Phase C: The Anonymous Inquiry**

Aegis sends only the five character prefix (2aae6) to the secure Have I Been Pwned database. Because millions of different passwords generate signatures starting with those same five letters, the database server has absolutely no way of knowing which password you are checking.

The database looks up its records and sends back a bucket of all compromised suffixes that match our prefix. The list you receive back in your browser will look similar to this:

35c94fcfb415dbe95f408b9ce91ee846ed:500  
8f20b33da2219c67cf8f41029baee24f91e:12  
1cd04faef32e7b165bc48a04df9ec310ef4:85

### **Phase D: The Local Match**

Now, completely inside your browser memory, Aegis searches this list. It notices that our private suffix (35c94fcfb415dbe95f408b9ce91ee846ed) is right there at the top.

Aegis flags this password as **Compromised** and reports that it has appeared in data leaks five hundred times.

## **🚀 How to Run the Portable Version (No Installation Required)**

This is the simplest way to run the tool without needing any technical setup:

1. Download the aegis.html file from this repository.  
2. Save it to a private folder on your computer.  
3. Double click aegis.html to open it instantly in your web browser.  
4. Go to the **Bulk CSV Audit** tab, paste or drag in your exported password list, map your columns, and click **Deploy Diagnostics Matrix** to begin.

## **🛡️ License**

This project is open source and released under the MIT License.