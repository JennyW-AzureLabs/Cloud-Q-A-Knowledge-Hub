# Why Organizations Use Microsoft Entra Domain Services

## 🌐 Overview
Microsoft Entra Domain Services (Entra DS or AAD DS) is **not** a more advanced version of Active Directory Domain Services (AD DS).  
Instead, it is a **managed service** that provides domain functionality **without domain controllers**.  

Organizations adopt it to **retire on-premises AD DS** while keeping **legacy apps** that still depend on old authentication methods like **Kerberos, NTLM, or LDAP**.

---

## 🧩 The Core Problem
Many companies moving to the cloud face a dilemma:

> “We want to shut down our on-prem AD servers, but our legacy applications still require a domain to authenticate users.”

These apps **cannot use** Microsoft Entra ID directly because Entra ID uses **modern cloud protocols** (OAuth2, OpenID Connect, SAML).  
Rewriting or modernizing those apps is often costly and risky.

---

## ⚙️ The Entra DS Solution
Microsoft Entra Domain Services acts as a **bridge** between the cloud and legacy systems.

- Microsoft **hosts and maintains** the domain controllers.  
- You get **Kerberos, NTLM, and LDAP** support inside Azure.  
- Azure VMs can **join the domain** just like on-prem PCs.  
- No need for **VPNs or hybrid sync infrastructure** to keep AD alive.

It’s like having your **old domain recreated in the cloud**, without the burden of managing it.

---

## 💼 Why Organizations Choose It

| Motivation | Benefit from Entra Domain Services |
|-------------|------------------------------------|
| 🧰 **Retire on-prem servers** | Microsoft manages domain controllers for you. |
| 🔒 **Simplify security** | Removes inbound VPN or AD replication risks. |
| 🧳 **Cloud migration** | Allows “lift and shift” of legacy domain-joined apps. |
| 🔁 **Hybrid coexistence** | Works with Microsoft Entra ID for modern identity. |
| ⏳ **Transition period** | A bridge while apps are modernized. |

---

## ⚠️ The Trade-offs
Entra DS simplifies operations, but with limitations compared to AD DS:

| Capability | AD DS | Entra DS |
|-------------|--------|-----------|
| Full OU hierarchy | ✅ | ❌ Flat only |
| Schema extensions | ✅ | ❌ Not supported |
| Domain Admin access | ✅ | ❌ Not available |
| Forest/domain trusts | ✅ | ❌ Not supported |
| Custom domain controllers | ✅ | ❌ Managed by Microsoft |

**In short:** You trade **control** for **convenience**.

---

## 🧠 Key Takeaway
> Microsoft Entra Domain Services is a **compatibility layer**, not a replacement.  
> It keeps legacy systems alive while the organization transitions fully to the cloud.

When your applications are fully modernized and can use **Microsoft Entra ID** directly,  
you won’t need Entra DS anymore.
