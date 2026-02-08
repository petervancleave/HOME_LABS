
### 3.3.1 Performing a Phishing Attack

In this lab, you will learn to perform a phishing attack. Phishing is a technique based on social engineering. With phishing, users are requested (usually through email or other websites) to supply personal information. Nearly 100 percent of email users have received phishing emails. Posing as legitimate emails, these fake emails are used to encourage the email recipient to click a link, download a file, or even call a number so that the attacker can steal credentials or data, plant malware, or contact them with another malicious intent. To perform a phishing attack, here's what you need to do:

1. From the left sidebar, click the **Terminal** icon.
2. In the **Terminal** window, execute the following command to stop the **Apache2** web server:
```
service apache2 stop
```

3. In the **Terminal** window, execute the following command to get the IP address:

```
ifconfig eth0 | grep "inet"
```

4. Write down the IP address:

5. Close the **Terminal** window.
6. From the left sidebar, click the **Terminal** icon.
7. In the **Terminal** window, execute the following commands one at a time:
```
setoolkit
y
1
2
3
1
```

Where,

- `setoolkit`: Starts the social engineering toolkit
- `y`: Accepts the terms and conditions
- `1`: Starts the process
- `2`: Selects Website Attack Vectors
- `3`: Selects the Credential Harvester Attack Method
- `1`: Selects Web Templates

7. Now, type the **IP address** that you noted in the text block at **Step 4** and press **Enter**.

8. In the **Terminal** window, type the following to select **Google**: `2`
9. From the left sidebar, click the **Firefox ESR** icon.
10. Navigate to the following URL `_http://IP address_`
11. Provide **Email** as `_john12@mail.com_` and **Password** as _`john123456`_ and click **Sign in**.
12. You will observe the **Google** page.
13. Minimize the **Firefox ESR** window.
14. Navigate to the **Terminal** window and you will observe that there will be a number of exploits in the **Terminal** window. You will also see the email and password you have entered at **Step 12**.
15. **Important:** Press **Ctrl+C** to stop the attack.
16. Close all windows.