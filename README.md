<div align="left" dir="ltr">
  <a href="README.md"><img src="https://img.shields.io/badge/English-007ec6?style=for-the-badge" alt="English"></a>
  <a href="README-Fa.md"><img src="https://img.shields.io/badge/Persian-2ea44f?style=for-the-badge" alt="Persian"></a>
</div>

# 📧 Comprehensive Guide to Setting Up Free Custom Domain Email (Connected to Gmail)

This guide will walk you through setting up a professional email address with your custom domain (e.g., `info@yourdomain.com`) completely free of charge, allowing you to send and receive emails directly through your **personal free Gmail inbox**. 
This method uses **ImprovMX** for receiving and forwarding emails, and **Google (Gmail SMTP)** servers for sending emails.

---

## 🛠️ Prerequisites
Before starting, make sure you have the following ready:

1. A custom domain name (e.g., `yourdomain.com`).
2. Access to your domain's DNS management panel (e.g., Cloudflare, Namecheap, or your hosting provider).
3. A personal Gmail account (e.g., `youraccount@gmail.com`).

---

## 📥 Part 1: Receiving Email Settings (Forwarding to Gmail via ImprovMX)

ImprovMX acts as a mail router; it receives emails sent to your custom domain address and instantly forwards them to your personal Gmail account.

### Step 1: Sign Up on ImprovMX

1. Go to [ImprovMX.com](https://improvmx.com).
2. Enter your domain name (`yourdomain.com`) and your personal Gmail address (`youraccount@gmail.com`).
3. Click the **Create a free forward** button.
4. Open your Gmail inbox and click the activation link sent by ImprovMX to verify your account.

### Step 2: Configure DNS Records in Cloudflare or Domain Panel
Log in to your domain's DNS management panel and add the following records to route your emails correctly:

| Record Type | Name / Host | Value | Priority | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **MX** | `@` (or leave blank) | `mx1.improvmx.com.` | `10` | Primary inbound mail server |
| **MX** | `@` (or leave blank) | `mx2.improvmx.com.` | `20` | Secondary inbound mail server |
| **TXT** | `@` (or leave blank) | `v=spf1 include:spf.improvmx.com ~all` | — | Prevents emails from being marked as spam |

> ⏳ **Note:** DNS changes can take anywhere from a few minutes to a few hours to propagate. In the ImprovMX dashboard, click **Check MX settings** until the status turns green (**Email forwarding active**).

---

## 📤 Part 2: Sending Email Settings (via Gmail SMTP Server)

Since the free tier of ImprovMX only forwards incoming emails, we use Google's outgoing SMTP servers so you can send emails using your custom domain identity.

### Step 1: Generate a Google App Password
Due to Google's security policies, you cannot use your standard Gmail password for SMTP connections; you must generate a dedicated App Password:

1. Go to your [Google Account Management](https://myaccount.google.com) page.
2. From the navigation menu, select the **Security** tab.
3. Make sure **2-Step Verification** is turned **ON** for your account.
4. In the search box at the top of the Security page, type **App passwords** and click on the result to go directly to the App Passwords creation page.
5. Enter a custom name for the app (e.g., `Custom Domain SMTP`).
6. Click **Create**. Copy and save the **16-character yellow password** displayed (ignore the spaces between letters).

### Step 2: Connect Domain to Gmail Inbox

1. Log in to your personal Gmail account.
2. Click the gear icon (Settings) in the top-right corner and select **See all settings**.
3. Go to the **Accounts and Import** tab.
4. In the **Send mail as** section, click **Add another email address**.
5. A yellow pop-up window will appear; fill in the details as follows:
   * **Name:** Your name or business name (e.g., `John Doe`).
   * **Email address:** Your custom domain email address (e.g., `info@yourdomain.com`).
   * ⚠️ **CRITICAL:** Make sure to **UNCHECK** the **Treat as an alias** option.
   * Click the **Next Step** button.

### Step 3: Enter Outgoing Server Details (SMTP)
Fill in the server details exactly as shown below:

* **SMTP Server:** `smtp.gmail.com`
* **Port:** `587`
* **Username:** Your full personal Gmail address (`youraccount@gmail.com`)
* **Password:** The **16-character App Password** you generated in Step 1.
* **Connection Type:** Select **Secured connection using TLS (recommended)**.

Finally, click the **Add Account** button.

### Step 4: Final Verification & Activation

1. Google will send a verification code to your custom domain email address to verify ownership.
2. Since incoming forwarding (Part 1) is already active, this email will automatically land in your personal Gmail inbox.
3. Open the email, copy the verification code, paste it into the yellow pop-up window, and click **Verify**.

---

## 🚀 Usage and Testing
Now, whenever you click **Compose** in Gmail, you will find a drop-down menu in the **From** field. You can easily choose whether to send your email from your personal Gmail address or using your professional custom domain identity.
