# 🔐 Azure AD Identity Protection

## 📝 Summary

This project demonstrates the implementation of **Azure Active Directory (Azure AD) Identity Protection** by configuring demo users, enabling **Multi-Factor Authentication (MFA)**, and enforcing a **Conditional Access Policy** to restrict login access from outside a specific region (e.g., the United States). The goal is to simulate real-world identity protection scenarios and provide a hands-on learning experience in managing Azure security controls.

---

## 📘 Topics Covered

- Azure Active Directory (AAD) user management
- Multi-Factor Authentication (MFA) configuration
- Conditional Access Policies
- Sign-in logs and monitoring
- Identity Protection best practices

---

## 💡 Scenario

A company wants to secure its cloud environment by:
- Creating test users.
- Enforcing MFA for specific users.
- Blocking access to users attempting to log in from outside approved geographic locations.

You’ll simulate this setup using two demo users and enforce region-based conditional access.

---

## ⚙️ Step-by-Step Guide

### 1. 👥 Create Demo Users

1. Navigate to: `Azure Portal → Azure Active Directory → Users → + New User`
2. Create two users:
   - `az900user1@yourtenant.onmicrosoft.com`
   - `az900user2@yourtenant.onmicrosoft.com`
3. Uncheck “Auto-generate password” and set custom passwords for both.

---

### 2. 🔐 Enable MFA for User1

1. Go to: `Azure AD → Users → Select az900user1`
2. Click on **Multi-Factor Authentication**.
3. In the MFA portal:
   - Select `az900user1`.
   - Click **Enable** → Confirm.

---

### 3. 🛑 Create Conditional Access Policy

1. Navigate to: `Azure AD → Security → Conditional Access → + New policy`
2. Configure the policy:
   - **Name**: `Block-Outside-US`
   - **Users**: Select → `az900user1`
   - **Cloud apps**: All cloud apps
   - **Conditions**:
     - Locations → Configure → Yes
     - **Include**: Any location
     - **Exclude**: United States *(or your region)*
   - **Access controls**: Grant → Block access
   - Enable policy → **On** → Click **Create**

---

### 4. 🔍 Test the Policy

- Attempt to sign in as `az900user1` from a VPN located outside your country.
- Access should be blocked based on the Conditional Access Policy.

---

### 5. 📊 Review Sign-in Logs

1. Go to: `Azure AD → Sign-in logs`
2. Filter by **User**: `az900user1`
3. Analyze logs for blocked attempts and conditional access events.

---

### 🧹 Cleanup

- Delete the test users:
  - `Azure AD → Users → Delete az900user1 and az900user2`
- Disable or delete the Conditional Access Policy:
  - `Azure AD → Conditional Access → Select and delete Block-Outside-US`
