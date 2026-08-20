# Lab 01: Automated Lifecycle Management & Group Rules

## 🎯 Objective
Automate user provisioning and group membership assignment in Okta using custom user profile attributes and Okta Expression Language (OEL), eliminating manual administrative intervention and reducing the risk of orphaned permissions.

---

## 🏗️ Architecture & Scenario
In modern cloud-native environments, manual user management is a major security vulnerability and a drain on IT resources. This lab establishes an automated onboarding pipeline:
1. **Custom Metadata:** Define extended profile attributes (such as `Department`) to capture precise organizational context.
2. **Dynamic Evaluation:** Configure an automated group rule to continuously evaluate user attributes against defined logic statements.
3. **Automated State Transition:** Instantly provision users into targeted security groups the moment their profile attributes match corporate policies.

---

## ⚙️ Configuration Steps

### 1. Custom Profile Attributes
* Navigated to **Directory** > **Profile Editor** > **User (default)**.
* Added a custom attribute to capture employee/contractor metadata:
  * **Display Name:** `Department`
  * **Variable Name:** `department`
  * **Data Type:** `String`

### 2. Target Security Group Creation
* Navigated to **Directory** > **Groups** and created a dedicated security group named `Contractors-Group` to house all active contractor accounts.

### 3. Dynamic Group Rule Construction
* Went to **Directory** > **Groups** > **Rules** and created a rule named `Contractor-Auto-Assignment`.
* Linked the rule to `Contractors-Group`.
* Configured the Okta Expression Language definition to filter users dynamically:
  ```text
  user.department == "Contractor"

  🧪 Validation & Testing
Test Execution: Created a test user profile (test.contractor@homelab.com) with the department attribute explicitly set to Contractor.

Verification Result: The Okta Identity Engine instantly evaluated the attribute upon creation and successfully mapped the user to the target group automatically.

💡 Key Takeaways & Challenges
Attribute Mapping: Ensured custom schema variables match seamlessly between profile definitions and expression rules.

Operational Impact: Automated group rules drastically minimize administrative overhead while ensuring zero-trust adherence to least-privilege access boundaries from day one.
