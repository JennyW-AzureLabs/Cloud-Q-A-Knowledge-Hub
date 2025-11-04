# Migrating from AD DS to Microsoft Entra ID – Application Isolation Model

### 🧭 Overview
When migrating from **Active Directory Domain Services (AD DS)** to **Microsoft Entra ID (Azure AD)**, one major conceptual shift is **how applications are isolated and managed**.  
AD DS relies on **Organizational Units (OUs)** and **Group Policies (GPOs)**, while Entra ID uses **object-based identity management** built around **service principals**.

Understanding this difference is key to planning a successful migration.

---

## 🏛️ AD DS: Hierarchical Isolation

In the on-premises world, **AD DS** organizes resources through a **tree-like structure**:
- **OUs (Organizational Units)** contain users, computers, or groups.
- **Group Policy Objects (GPOs)** apply security and configuration rules.
- Applications can be isolated by assigning them to specific OUs or applying policies that control access.

**Example:**
corp.local
├── HR-OU → HR App Policy
├── Finance-OU → Finance App GPO
└── IT-OU → Admin Rights


Isolation in AD DS depends on **hierarchical folders** and **linked policies**.

---

## ☁️ Entra ID: Object-Based Isolation

In the **cloud**, there are **no OUs or GPOs**.  
Instead, Microsoft Entra ID uses a **flat structure** where each entity—user, device, group, or app—is represented by an **object** with its own permissions and identity.

### 🔹 Service Principals: The Core of App Isolation

A **Service Principal** is the **identity of an application inside your Entra tenant**.  
It functions like a user account for the app itself, allowing it to **authenticate** and **access resources** securely.

When you:
1. **Register** an app in Entra ID → creates an **Application object** (the blueprint).
2. **Grant** access in your tenant → creates a **Service Principal object** (the active instance).

Each service principal:
- Has its own credentials (client secret or certificate)
- Is assigned specific roles and permissions
- Operates **independently** of other apps

This **object-level isolation** replaces the folder-based separation of AD DS.

---

## 🔐 Why Microsoft Changed the Model

| Reason | AD DS (On-Premises) | Entra ID (Cloud-Based) |
|--------|----------------------|-------------------------|
| **Architecture** | Hierarchical (OUs) | Flat (Objects & Relationships) |
| **Policy Management** | Group Policy Objects | Conditional Access & App Roles |
| **App Identity** | Shared service accounts | Dedicated Service Principals |
| **Security Basis** | Network-bound | Token-based (OAuth, OpenID Connect) |
| **Isolation Mechanism** | Folder & Policy | Object & Permission Scope |

Microsoft re-engineered identity for the cloud because:
- Resources are distributed across regions and devices.  
- Each app or service needs its own **secure identity boundary**.  
- Fine-grained, auditable control scales better than GPO inheritance.

---

## 🧩 Example in Azure Portal

**Path:**  
`Microsoft Entra ID → Enterprise Applications → [App Name]`

Each application listed represents a **Service Principal** with:
- Sign-in and audit logs  
- Granted permissions  
- Role assignments  

Each one is a **separate, isolated identity** — ensuring security at the application level.

---

## 🧠 Migration Tip

| If you used this in AD DS... | You’ll use this in Entra ID... |
|------------------------------|--------------------------------|
| OUs for organizing apps | Enterprise Applications (Service Principals) |
| GPOs for access control | Conditional Access policies |
| Shared service accounts | Managed Identities or App Registrations |
| Network-based access | Token-based access (OAuth2.0 / OpenID) |

---

## 📘 Key Takeaway

When migrating to Microsoft Entra ID, remember that:
> **Application isolation is achieved through Service Principals — not OUs.**

Each app gets its own **identity object**, **credentials**, and **permissions**, creating a cleaner, more secure model built for cloud-native management.
