# Enforcing Strong Passwords

## Lab Objective
The objective of this lab is to learn how to force users to create strong passwords.

## Lab Purpose
You have firewalls and virus scanners, but all this protection is negated if your password is cracked. That is where strong passwords come in. A strong password is difficult to guess using manual and automatic password cracking tools.

## Lab Tool
- Virtual PC running Windows 10 Pro or Enterprise (Windows 10 Home does not include the Local Security Policy tool).

## Prerequisites
- You are signed in with an administrator account.
- The VM is a standalone (non-domain) machine, so no Group Policy overrides the local settings.

## Lab Topology
Single Windows 10 virtual machine (standalone, no network dependencies).

---

## Lab Walkthrough

### Task 1: Open Local Security Policy

Click the search bar (or press Windows key) and type:

```text
secpol.msc
```

Right-click the result and choose Run as administrator.

### Task 2: Navigate to the Password Policy

In the left pane, expand Security Settings, then Account Policies.

Click Password Policy.

Double-click Store passwords using reversible encryption and make sure it is set to Disabled. (Reversible encryption is effectively the same as storing passwords in plain text, so it should stay off.) Click OK.

### Task 3: Open the Complexity Setting

Double-click Password must meet complexity requirements.

### Task 4: Read the Explanation, Then Enable the Policy

Click the Explain tab and read it. Note the rules it lists:

- The password cannot contain the user’s account name or parts of the full name that exceed two consecutive characters.
- It must contain characters from at least three of these four groups: uppercase letters, lowercase letters, numbers, and symbols.

Click back on the Local Security Setting tab and select the Enabled radio button.

Click Apply, then OK.

### Task 5: Set a Minimum Password Length

Complexity alone does not control length, so set it as well.

In the same Password Policy list, double-click Minimum password length.

Set it to 12 characters.

Click Apply, then OK.

### Task 6: Test the Policy (Required)

Open Command Prompt as administrator (search cmd, right-click, Run as administrator).

Try to create a user with a weak password:

```cmd
net user testuser password /add
```

**Expected result:** the command fails with an error stating the password does not meet the password policy requirements.

Create the user with a strong password:

```cmd
net user testuser Str0ng!Passw0rd#42 /add
```

**Expected result:** “The command completed successfully.”

Verify the account exists:

```cmd
net user
```

Take a screenshot of the failed and successful attempts as evidence.

### Task 7: Cleanup

Remove the test account:

```cmd
net user testuser /delete
```

---

## Notes

You can use evaluation versions of Windows for free on your virtual machines.

Existing passwords are not affected until they are next changed.

Modern guidance (e.g., NIST SP 800-63B) favors long passphrases and screening against breached-password lists over rigid complexity rules alone.

---

## Conclusion

This lab explores how to enforce stronger password requirements in Windows using Local Security Policy, including password complexity, minimum password length, and verification through user account creation.
