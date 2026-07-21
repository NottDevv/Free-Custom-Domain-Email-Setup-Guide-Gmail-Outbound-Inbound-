<div align="left" dir="ltr">
  <a href="README.md"><img src="https://img.shields.io/badge/English-007ec6?style=for-the-badge" alt="English"></a>
  <a href="README-Fa.md"><img src="https://img.shields.io/badge/Persian-2ea44f?style=for-the-badge" alt="Persian"></a>
</div>

# 📧 Free Custom Domain Email Setup Guide (Gmail Outbound & Inbound)

This guide provides a comprehensive, step-by-step walkthrough to configure a professional business email using your **custom domain** entirely for free. We will leverage **ImprovMX** for free inbound email forwarding and **Gmail's SMTP servers** for secure outbound email delivery.

---

## 🛠️ Prerequisites
Before starting, ensure you have:
1. A custom domain (e.g., `yourdomain.com`).
2. Access to your domain's DNS manager (e.g., Cloudflare, Namecheap, IRNIC).
3. A personal Gmail account (e.g., `youraccount@gmail.com`).

---

## 📥 Phase 1: Inbound Setup (Receiving Emails via ImprovMX)

ImprovMX acts as a router that catches emails sent to your business alias and forwards them straight to your personal Gmail inbox.

### Step 1: Register on ImprovMX
1. Go to [ImprovMX.com](https://improvmx.com).
2. Enter your custom domain (`yourdomain.com`) and your personal Gmail (`youraccount@gmail.com`).
3. Click **Create a free forward**.
4. Check your Gmail inbox and click the verification link to activate your account.

### Step 2: Configure Domain DNS Records
Log in to your DNS provider (e.g., Cloudflare) and add the following records to route your emails properly:

| Type | Name / Host | Value | Priority | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **MX** | `@` (or blank) | `://improvmx.com.` | `10` | Primary Mail Server |
| **MX** | `@` (or blank) | `://improvmx.com.` | `20` | Secondary Mail Server |
| **TXT** | `@` (or blank) | `v=spf1 include:://improvmx.com ~all` | — | SPF record (Prevents spoofing) |

> ⏳ **Note:** DNS propagation can take anywhere from a few minutes to a few hours. Go to your ImprovMX dashboard and click **Check MX settings**. Ensure the status turns green (**Email forwarding active**).

---

## 📤 Phase 2: Outbound Setup (Sending Emails via Gmail SMTP)

Since ImprovMX only handles incoming traffic, we configure Gmail's native SMTP servers to send emails outward using your brand identity.

### Step 1: Generate a Google App Password
Due to modern security constraints, you cannot use your main Gmail password for external SMTP authentication. You must generate an App Password.

1. Go to your [Google Account Management](https://google.com) panel.
2. Navigate to the **Security** tab on the left.
3. Ensure **2-Step Verification** is turned **ON** for your account.
4. Click on **2-Step Verification** again, scroll down to the bottom, and click on **App passwords**.
5. Give the password a custom identifier name (e.g., `Custom Domain SMTP`).
6. Click **Create**. Copy the generated **16-character password code** (ignore spaces) and save it securely.

### Step 2: Connect the Custom Domain to Gmail
1. Open your personal Gmail inbox.
2. Click the **Gear Icon** (Settings) in the top-right corner -> Select **See all settings**.
3. Move to the **Accounts and Import** tab.
4. Under the **Send mail as** section, click **Add another email address**.
5. A yellow configuration pop-up window will appear:
   * **Name:** Your professional or brand name (e.g., `John Doe`).
   * **Email address:** Your professional alias (e.g., `info@yourdomain.com`).
   * ⚠️ **Crucial:** **Uncheck** the box that says **Treat as an alias**.
   * Click **Next Step**.

### Step 3: Input Server Authentication Details
Carefully fill out the SMTP credential fields exactly as specified below:

* **SMTP Server:** `://gmail.com` *(Do not add slashes or protocols like `://`)*
* **Port:** `587`
* **Username:** Your complete personal Gmail address (`youraccount@gmail.com`)
* **Password:** The **16-character App Password** code generated during Step 1.
* **Connection Security:** Select **Secured connection using TLS (recommended)**.

Click **Add Account**.

### Step 4: Final Verification Code
1. Google will send a confirmation code to verify domain ownership.
2. Since Phase 1 is already complete, this verification code will be forwarded directly to your personal Gmail inbox.
3. Open the email, copy the numerical verification code, paste it into the yellow pop-up window, and click **Verify**.

---

## 🚀 Usage & Testing
When composing a new message in Gmail, click on the **From** field dropdown menu. You can now toggle seamlessly between your personal address and your custom business email.

---

## 📄 License & Attribution
This setup relies on the free tier offerings of Google Accounts and ImprovMX. Feel free to fork or modify this guide to help other developers launch their MVP communication infrastructures cleanly.
