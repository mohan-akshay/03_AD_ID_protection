# 🔐 Azure AD Identity Protection

## 📝 Summary

This project demonstrates the implementation of **Azure Active Directory (Azure AD) Identity Protection** by configuring demo users, enabling **Multi-Factor Authentication (MFA)**, and enforcing a **Conditional Access Policy** to restrict login access from outside a specific region (e.g., the United Kingdom). The goal is to simulate real-world identity protection scenarios and provide a hands-on learning experience in managing Azure security controls.

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

I am going to simulate this setup using two demo users and enforce region-based conditional access.

---

## ⚙️ Step-by-Step Guide

### 1. 👥 Create Demo Users

1. Navigate to: `Azure Portal → Azure Entra ID → Users → + New User`
2. Create two users:
   - `demouser1@my_tenant.onmicrosoft.com`
   - `demouser2@my_tenant.onmicrosoft.com`
3. Uncheck “Auto-generate password” and set custom passwords for both.

---

### 2. 🔐 Enable MFA for User1

1. Go to: `Azure AD → Users → Select demouser1`
2. Click on **per user MFA**.
3. In the MFA portal:
   - Select both users.
   - Click **Enable** → Confirm.

---

### 3. 🛑 Create Conditional Access Policy

1. Navigate to: `Azure AD → Security → Conditional Access → + New policy`
2. Configure the policy:
   - **Name**: `Block-Outside-UK`
   - **Users**: Select → `demouser1`
   - **Cloud apps**: All cloud apps
   - **Conditions**:
     - Locations → Configure → Yes
     - **Include**: Any location
     - **Exclude**: United Kingdom *(or your region)*
   - **Access controls**: Grant → Block access
   - Enable policy → **On** → Click **Create**

---

### 4. 🔍 Test the Policy

- Attempt to sign in as `demouser1` from a VPN located outside your country.
- Access should be blocked based on the Conditional Access Policy.

---

### 5. 📊 Review Sign-in Logs

1. Go to: `Azure AD → Sign-in logs`
2. Filter by **User**: `demouser1`
3. Analyze logs for blocked attempts and conditional access events.
4. We can also check other sign in activities and log status here.

---

### 🧹 Cleanup

- Delete the test users:
  - `Azure AD → Users → Delete demouser1 and demouser2`
- Disable or delete the Conditional Access Policy:
  - `Azure AD → Conditional Access → Select and delete Block-Outside-UK`
